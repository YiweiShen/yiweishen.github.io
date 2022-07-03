---
title: Progress Display for ftplib using Rich Library in Python
date: 2022-07-03 10:44:57
tags: python
---

The ftplib is included in Python batteries, which can be used to implement the client side of the FTP protocol. It's compact and easy to use, but missing a user-friendly progress display. For example, if you have a long-time connection to upload / download a large file to / from the FTP server, the terminal tells you nothing about the progress of the file transfer.

Don't panic.

Luckily, we have Rich, a Python library, showing rich text (with color and style) to the terminal. Especially, it can display continuously updated information regarding the progress of long running tasks / file copies etc. That is perfect for the scenario of file transfer with FTP server.

The main challenge is that the Progress in rich.progress has to be called every time you need to update the UI and we have to, at the same time, synchronize the actual progress of FTP file transfer.

OK, show me the code.

First, make sure you have rich library installed. 

Then, double check if you get these dependencies imported.

```python
import time
from ftplib import FTP_TLS
from rich import print
from rich.progress import Progress, SpinnerColumn, TotalFileSizeColumn, TransferSpeedColumn, TimeElapsedColumn
```

The implementation is straightforward with the help from the callback in FTP.retrbinary(). The callback function is called for each block of data received. And that is when we take the chance to update and render the progress display.

Here is an example of downloading from FTP server.

```python
def download_from_ftp(file_path):
    # ftplib.FTP_TLS() connects to FTP server with username and password
    ftp = FTP_TLS(host=FTP_HOST, user=FTP_USER, passwd=FTP_PASSWD)

    # Securing the data connection requires the user to explicitly ask for it by calling the prot_p()
    ftp.prot_p()

    # prepare a file object on local machine to write data into
    f = open(file_path, 'wb')

    # initialize the ftp_progress with file_size, ftp connection and the file object
    # you may need to work out how to get the actual file size
    # Hint: FTP.dir() produces a directory listing as returned by the LIST command
    tracker = ftp_progress(file_size, ftp, f)

    # the trick to update rich progress display is using the callback function in retrbinary()
    ftp.retrbinary('RETR example_file.zip', callback=tracker.handle)
    
    # stop progress display and also terminate the file object
    tracker.stop()

    # send a QUIT command to the server and close the connection
    ftp.quit()
```

If you go through the comments I wrote for the above function, then the below class should be fairly self-explanatory to you. The handle() is where we reflect the changes in each iteration, yes in callbacks.

One thing you should be aware of is that FTP uses two separate TCP connections: one to carry commands and the other to transfer data. So in the case of a long-time file transfer, you need to talk to the command channel once a while, to keep it connected. 'NOOP' command is designed for this, to prevent the client from being automatically disconnected (by server) for being idle.

```python
class ftp_progress:
    def __init__(self, file_size, ftp, f):
        self.file_size = file_size
        self.ftp = ftp
        self.f = f
        self.size_written = 0
        self.time = time.time()
        self.progress = Progress(
            SpinnerColumn(),
            *Progress.get_default_columns(),
            TotalFileSizeColumn(),
            TransferSpeedColumn(),
            TimeElapsedColumn(),
        )
        self.task_download = self.progress.add_task("[red]Download...", total=self.file_size)
        self.progress.start()

    def stop(self):
        self.progress.stop()
        self.f.close()
        
    def handle(self, data):
        self.f.write(data)
        self.size_written += 8192
        self.progress.update(self.task_download, advance=8192)

        # keep FTP control connection alive
        if time.time() - self.time > 60:
            self.time = time.time()
            self.ftp.putcmd('NOOP')
```

As a final note, it should be mentioned that be careful of passing by reference in Python. If you don't close / keep FTP connections correctly with the server, strange things (not the TV show) cound happen.

And, stay away from the nested callbacks, always.

Ref:

ftplib — FTP protocol client
https://docs.python.org/3/library/ftplib.html

Rich’s documentation
https://rich.readthedocs.io/en/stable/index.html

Progress Display (Rich)
https://rich.readthedocs.io/en/stable/progress.html