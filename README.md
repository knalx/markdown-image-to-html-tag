# markdown-image-to-html-tag
Convert Markodown image link to html tag with size

# Why?
By default if you paste an image on Github PR creation page from clipboard, it paste it as a markdown link. e.g.:
```
![image](https://user-images.githubusercontent.com/4751234/1234.png)
```
It does not have a format options, so on preview it shows a giant image that covers the whole page and it doesn’t look nice.

This small JS script wraps input on github creation page to a html `img` tag and set `height` of the image. Like this:
```
<img src=https://user-images.githubusercontent.com/4751191/1234.png height="400">
```

# Script
```
javascript:(function(){var prTextElement=document.querySelector('textarea[name="pull_request[body]"]');var issueTextElement=document.querySelector('textarea[name="issue[body]"]');var textAreaInput=prTextElement;if(!textAreaInput){textAreaInput=issueTextElement}const regexp=new RegExp(/(\!\[image.*(http.*png)\))/,'g');function replacer(match,p1,p2){const max_img_height=400;return`<img src=${p2} height=\"${max_img_height}\">`}var issueBody=textAreaInput.value.trim();textAreaInput.value=issueBody.replaceAll(regexp,replacer)})();
```

# How to use?
You can add it to you bookmark and execute during editing of the PR text. It will replace images with tags and keep other content as it is.

> Note: You may need to adjust a regexp img name for other OS’s, and replace `\[image.`
> with something else. Also you can configure an `max_img_height`
