<!---
    Licensed to the Apache Software Foundation (ASF) under one
    or more contributor license agreements.  See the NOTICE file
    distributed with this work for additional information
    regarding copyright ownership.  The ASF licenses this file
    to you under the Apache License, Version 2.0 (the
    "License"); you may not use this file except in compliance
    with the License.  You may obtain a copy of the License at

      http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing,
    software distributed under the License is distributed on an
    "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY
    KIND, either express or implied.  See the License for the
    specific language governing permissions and limitations
    under the License.
-->

# org.apache.cordova.dialogs

这个插件提供了对一些本机对话框的用户界面元素的访问。

## 安装

    cordova plugin add org.apache.cordova.dialogs
    

## 方法

*   `navigator.notification.alert`
*   `navigator.notification.confirm`
*   `navigator.notification.prompt`
*   `navigator.notification.beep`

## navigator.notification.alert

显示一个自定义的警报或对话框框。 大多数科尔多瓦实现使用本机对话框中的此项功能，但一些平台使用浏览器的 `alert` 函数，这是通常不那么可自定义。

    navigator.notification.alert(message, alertCallback, [title], [buttonName])
    

*   **消息**： 消息对话框。*（字符串）*

*   **alertCallback**： 当警报对话框的被解雇时要调用的回调。*（函数）*

*   **标题**： 标题对话框。*（字符串）*（可选，默认值为`Alert`)

*   **buttonName**： 按钮名称。*（字符串）*（可选，默认值为`OK`)

### 示例

    function alertDismissed() {
        // do something
    }
    
    navigator.notification.alert(
        'You are the winner!',  // message
        alertDismissed,         // callback
        'Game Over',            // title
        'Done'                  // buttonName
    );
    

### 支持的平台

*   亚马逊火 OS
*   Android 系统
*   黑莓 10
*   火狐浏览器操作系统
*   iOS
*   Tizen
*   Windows Phone 7 和 8
*   Windows 8

### Windows Phone 7 和 8 怪癖

*   有没有内置浏览器警报，但你可以绑定一个，如下所示调用 `alert()` 在全球范围内：
    
        window.alert = navigator.notification.alert;
        

*   两个 `alert` 和 `confirm` 的非阻塞的调用，其中的结果才是可用的异步。

### 火狐浏览器操作系统怪癖：

这两个本机阻止 `window.alert()` 和非阻塞 `navigator.notification.alert()` 可用。

## navigator.notification.confirm

显示一个可自定义的确认对话框。

    navigator.notification.confirm(message, confirmCallback, [title], [buttonLabels])
    

*   **消息**： 消息对话框。*（字符串）*

*   **confirmCallback**: 要用索引 （1、 2 或 3） 按下的按钮，或者在没有按下按钮 (0) 驳回了对话框中时调用的回调。*（函数）*

*   **标题**： 标题对话框。*（字符串）*（可选，默认值为`Confirm`)

*   **buttonLabels**： 指定按钮标签的字符串数组。*（数组）*（可选，默认值为 [ `OK,Cancel` ])

### confirmCallback

`confirmCallback`当用户按下确认对话框中的按钮之一的时候执行。

回调将参数 `buttonIndex` *（编号）*，它是按下的按钮的索引。 请注意索引使用基于 1 的索引，所以值是 `1` ， `2` ， `3` ，等等。

### 示例

    function onConfirm(buttonIndex) {
        alert('You selected button ' + buttonIndex);
    }
    
    navigator.notification.confirm(
        'You are the winner!', // message
         onConfirm,            // callback to invoke with index of button pressed
        'Game Over',           // title
        ['Restart','Exit']     // buttonLabels
    );
    

### 支持的平台

*   亚马逊火 OS
*   Android 系统
*   黑莓 10
*   火狐浏览器操作系统
*   iOS
*   Tizen
*   Windows Phone 7 和 8
*   Windows 8

### Windows Phone 7 和 8 怪癖

*   有没有内置的浏览器功能的 `window.confirm` ，但你可以将它绑定通过分配：
    
        window.confirm = navigator.notification.confirm;
        

*   调用到 `alert` 和 `confirm` 的非阻塞，所以结果就是只可用以异步方式。

### 火狐浏览器操作系统怪癖：

这两个本机阻止 `window.confirm()` 和非阻塞 `navigator.notification.confirm()` 可用。

## navigator.notification.prompt

显示本机的对话框，更可自定义的浏览器比 `prompt` 函数。

    navigator.notification.prompt(message, promptCallback, [title], [buttonLabels], [defaultText])
    

*   **消息**： 消息对话框。*（字符串）*

*   **promptCallback**: 要用索引 （1、 2 或 3） 按下的按钮，或者在没有按下按钮 (0) 驳回了对话框中时调用的回调。*（函数）*

*   **标题**： 对话框的标题*（字符串）* （可选，默认值为`Prompt`)

*   **buttonLabels**： 数组，这些字符串指定按钮标签*（阵列）* （可选，默认值为`["OK","Cancel"]`)

*   **defaultText**: 默认文本框中输入值 （ `String` ） （可选，默认值: 空字符串）

### promptCallback

`promptCallback`当用户按下一个提示对话框中的按钮时执行。`results`对象传递给回调的包含以下属性：

*   **buttonIndex**： 按下的按钮的索引。*（人数）*请注意索引使用基于 1 的索引，所以值是 `1` ， `2` ， `3` ，等等。

*   **输入 1**： 在提示对话框中输入的文本。*（字符串）*

### 示例

    function onPrompt(results) {
        alert("You selected button number " + results.buttonIndex + " and entered " + results.input1);
    }
    
    navigator.notification.prompt(
        'Please enter your name',  // message
        onPrompt,                  // callback to invoke
        'Registration',            // title
        ['Ok','Exit'],             // buttonLabels
        'Jane Doe'                 // defaultText
    );
    

### 支持的平台

*   亚马逊火 OS
*   Android 系统
*   火狐浏览器操作系统
*   iOS
*   Windows Phone 7 和 8

### Android 的怪癖

*   Android 支持最多的三个按钮，并忽略任何更多。

*   关于 Android 3.0 及更高版本，使用全息主题的设备按相反的顺序显示按钮。

### 火狐浏览器操作系统怪癖：

这两个本机阻止 `window.prompt()` 和非阻塞 `navigator.notification.prompt()` 可用。

## navigator.notification.beep

该设备播放提示音声音。

    navigator.notification.beep(times);
    

*   **时间**： 的次数重复发出蜂鸣音。*（人数）*

### 示例

    // Beep twice!
    navigator.notification.beep(2);
    

### 支持的平台

*   亚马逊火 OS
*   Android 系统
*   黑莓 10
*   iOS
*   Tizen
*   Windows Phone 7 和 8
*   Windows 8

### 亚马逊火 OS 怪癖

*   亚马逊火 OS 播放默认**设置/显示 & 声音**面板下指定的**通知声音**。

### Android 的怪癖

*   Android 系统播放的默认**通知铃声****设置/声音和显示**面板下指定。

### Windows Phone 7 和 8 怪癖

*   依赖泛型蜂鸣音文件从科尔多瓦分布。

### Tizen 怪癖

*   Tizen 通过播放音频文件通过媒体 API 实现会发出蜂鸣声。

*   蜂鸣音文件必须很短，必须设在 `sounds` 子目录中的应用程序的根目录中，并且必须命名`beep.wav`.