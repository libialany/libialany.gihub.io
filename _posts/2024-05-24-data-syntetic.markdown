---
title:  "Is synthetic!"
subtitle: "Introducing LittleFS"
author: "Lib"
avatar: "img/authors/wferr.png"
image: "img/data-syntetic.jpg"
date:   2024-06-06 11:30:00
---

### Description
<p style="font-size: 15px;">1. what is LittleFS?

In this article, we provide a brief description of LittleFS for ESP32. I think you know something about python in python work operation on SO , you have to use os, tempfile, and many.
LittleFS lets you access the flash memory like you would do in a standard file system on your computer.
</p>

### Let's practice

```
#include <Arduino.h>
#include "FS.h"
#include <LittleFS.h>
#define FORMAT_LITTLEFS_IF_FAILED true

void listDir(fs::FS &fs, const char * dirname, uint8_t levels){
    Serial.printf("Listing directory: %s\r\n", dirname);
    File root = fs.open(dirname);
    if(!root){
        Serial.println("- failed to open directory");
        return;
    }
    if(!root.isDirectory()){
        Serial.println(" - not a directory");
        return;
    }
    File file = root.openNextFile();
    while(file){
        if(file.isDirectory()){
            Serial.print("  DIR : ");
            Serial.println(file.name());
            if(levels){
                listDir(fs, file.path(), levels -1);
            }
        } else {
            Serial.print("  FILE: ");
            Serial.print(file.name());
            Serial.print("\tSIZE: ");
            Serial.println(file.size());
        }
        file = root.openNextFile();
    }
}

void setup(){
    Serial.begin(115200);
    if(!LittleFS.begin(FORMAT_LITTLEFS_IF_FAILED)){
        Serial.println("LittleFS Mount Failed");
        return;
    }
}

void loop(){
}
```

### Lastly

I love to learn few of my Esp32 🖍️



