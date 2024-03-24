---
title: Handle Login with Python Bindings for Selenium
date: 2024-03-23 22:52:12
tags:
---

Before everything else, you need to install the Selenium package, of course.

```bash
pip install selenium
```

Or, if you hate to deal with anti-bot measures, you can just use this.

```bash
pip install undetected-chromedriver
```

Then, add the user data directory to the ChromeOptions object. It is the path to your Chrome profile. For macOS, it is located at '~/Library/Application Support/Google/Chrome'.

```python
import undetected_chromedriver as uc

options = uc.ChromeOptions()
options.add_argument(f"--user-data-dir={'Path_to_your_Chrome_profile'}")
driver = uc.Chrome(options=options)

driver.get('https://www.example.com')
```

The `--user-data-dir` argument is kind of cheating because it allows you to bypass the login process without actually logging in.

Cookie is your friend.

But sometimes, you need to handle the login process, for instance, you have to switch between multiple accounts.

First of all, take care of your credentials. Use an .env file.

```python
import os
from dotenv import load_dotenv

load_dotenv()

USERNAME = os.getenv('USERNAME_ENV_VAR')
PASSWORD = os.getenv('PASSWORD_ENV_VAR')
```

Then, you can use the `send_keys` method to fill in the username and password fields. I add one while loop to wait for the element in case the script runs too fast.

```python
while True:
    try:
        driver.find_element(by=By.ID, value="username").send_keys(USERNAME)
        break
    except:
        time.sleep(1)

driver.find_element(by=By.ID, value="password").send_keys(PASSWORD)
driver.find_element(by=By.ID, value="submit").click()
```

After logging in, the chrome usally pops up a dialog asking if you want to save the password. It is annoying.

You can try to disable it by adding the `--disable-save-password-bubble` or `--disable-popup-blocking` argument to the ChromeOptions object. I don't think it works. But you can try.

In the end, I just used a hack, that is to open a new tab and immediately close it, the popup will appear.

```python
# open a new tab
driver.execute_script("window.open('','_blank')")

time.sleep(1) # 1 second wait is enough I guess
driver.switch_to.window(driver.window_handles[1])

# say goodbye to the new tab
driver.close()

# now switch back to the original tab
driver.switch_to.window(driver.window_handles[0])
```

That's it.

Oh, one more thing.

Add user-agent to the ChromeOptions object is also a good idea. And please do not forget to specify `version_main` for the driver to match your current chrome version.
