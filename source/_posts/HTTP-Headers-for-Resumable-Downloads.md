---
title: HTTP Headers for Resumable Downloads
date: 2024-04-22 23:14:18
tags:
---

We've all experienced the frustration of a poor internet connection. You may recall the disappointment of a large file download failing after 24 hours of waiting. Even worse, discovering that the download is not resumable.

Responsibility for resumable downloads doesn't solely rest on the client side with the correct setting of HTTP headers. It's equally, if not more, important for the backend to correctly enable several headers and implement the associated logic.

While I won't delve into the detailed implementation in a specific language, understanding the headers discussed below will equip you with the knowledge to easily implement this feature if you wish.

# Client

The only aspect you need to focus on is the Range HTTP request header. This header specifies the portions of a resource that the server should return. That's all there is to it.

```bash
Range: <unit>=<range-start>-
```

On the client side, the only requirement is to properly implement the Range HTTP request header. This involves using the correct unit and determining the starting point of the range. The server then knows which portion of the file to send. There's no need to worry about specifying the range end, as the typical use case involves resuming and downloading the entire file.

# Server

Now, things start to get more complicated.

The ETag (also known as entity tag) HTTP response header serves as an identifier for a specific version of a resource.

```bash
ETag: "<etag_value>"
```

If your target client includes a browser, then you need to set the ETag. Modern browsers expect to see this value; otherwise, the browser will simply retry downloading the entire file again.

The Content-Range response HTTP header signifies the position of a partial message within the full body message.

```bash
Content-Range: <unit> <range-start>-<range-end>/<size>
```

Imagine you are downloading a file of 500 bytes, but due to an unstable internet connection, the download is interrupted after only 100 bytes. In this scenario, you would expect the server to send the remaining 400 bytes of the file. Consequently, you would anticipate seeing the appropriate header in the server's response.

```bash
Content-Range: bytes 100-499/500
```

Check out MDN for understanding those numbers, I won't explain them here.

The Accept-Ranges HTTP response header acts as a signal from the server, indicating its capability to handle partial requests from the client for file downloads.

Essentially, this header communicates to the client, "Hey, I am capable of handling this, let's proceed."

Don't ask me why, you just need it.

```bash
Accept-Ranges: <range-unit>
```

I suggest simply using bytes.

```bash
Accept-Ranges: bytes
```

The Content-Length header signifies the size of the message body, measured in bytes, that is transmitted to the recipient.

In layman's terms, it represents the bytes of the remaining file.

```bash
Content-Length: <length>
```

Let's continue the same example mentioned above, the server is going to send the remaining 400 bytes of the file.

```bash
Content-Length: 400
```

This is merely an introduction.

There are many complex considerations to take into account. For instance, when dealing with ETags, you must strategize on how to assign a unique ID to each resource. Additionally, you need to determine how to update the ETag when a resource is upgraded to a newer version.

Understanding those HTTPS headers is a good start.
