---
author: Ashish
comments: true
date: 2008-04-15 14:40:24+00:00
layout: post
slug: serializing-xml-in-net-utf-8-and-utf-16
title: Serializing XML in .NET - UTF-8 and UTF-16
wordpress_id: 21
tags:
- csharp
- dotnet
- xml
---

When working with xml to object mapping, most modern languages have powerful tools or libraries that serialize and deserialize objects for you automatically, or even create classes for you based on xml schema definitions (XSDs). In the .NET world, these classes reside in the System.Xml.Serialization namespace. There is plenty of documentation available on how to use it.

However, you might encounter an issue when trying to serialize your object to XML, especially if you use a StringWriter to serialize your object to an XML string instead of a file. Since .NET strings are always stored in UTF-16, your resulting xml file will have the encoding of UTF-16. One way to get around this is by creating a MemoryStream, creating a StreamWriter, and applying the UTF-8 encoding to that StreamWriter.

The easy way of serializing an object to xml as a string (not to a file):

    
    XmlSerializer serializer = new XmlSerializer(typeof(YourObject));
    System.IO.StringWriter sWriter = new System.IO.StringWriter();
    
    serializer.Serialize(sWriter, yourObjectInstance);
    sWriter.Flush();
    
    string result = sWriter.ToString();


But since this will result in an xml file with encoding UTF-16, we have the following block:

    
    XmlSerializer serializer = new XmlSerializer(typeof(YourObject));
    
    // create a MemoryStream here, we are just working
    // exclusively in memory
    System.IO.Stream stream = new System.IO.MemoryStream();
    
    // The XmlTextWriter takes a stream and encoding
    // as one of its constructors
    System.Xml.XmlTextWriter xtWriter = new System.Xml.XmlTextWriter(stream, Encoding.UTF8);
    
    serializer.Serialize(xtWriter, yourObjectInstance);
    
    xtWriter.Flush();
    
    // go back to the beginning of the Stream to read its contents
    stream.Seek(0, System.IO.SeekOrigin.Begin);
    
    // read back the contents of the stream and supply the encoding
    System.IO.StreamReader reader = new System.IO.StreamReader(stream, Encoding.UTF8);
    
    string result = reader.ReadToEnd();


**Update 5/5/09** - From MumHaBR in the comments, instead of using the final StreamReader, you can use this:

    
    Encoding.UTF8.GetString(stream.ToArray());


Remember, the MemoryStream is just a stream of bytes and doesn't have to be text. So you create a StreamReader to read it back and have to tell the reader what encoding to use.

The idea of strings represented as bytes out in the wild, and various encodings, can be a little daunting for newer developers, but as long as you keep your encodings consistent, you should have no problems. And in the case that you need to convert to a different encoding, there are built-in libraries that do that for you.
