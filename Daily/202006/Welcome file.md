# StackEdit에 오신 것을 환영합니다!

안녕! ** StackEdit ** 의 첫 번째 마크 다운 파일입니다. StackEdit에 대한 배우입니다. 마크 다운입니다. 나와 함께 끝나면 탐색 모음의 왼쪽 모서리 에있는 ** 파일 탐색기 ** 를 열어서 새 파일을 만들 수 있습니다.


# 파일

StackEdit는 파일을 저장합니다. 즉, 모든 파일이 자동으로 로컬에 저장 되고 ** 오프라인에 액세스 할 수 있습니다! **

## 파일 및 폴더 생성

파일 탐색기는 탐색 모음의 옵션입니다. 파일 탐색기에서 ** 새 파일 ** 단추를 클릭하면 새 파일을 만들 수 있습니다. ** 새 폴더 ** 버튼을 클릭하면 폴더를 만들 수 있습니다.

## 다른 파일로 전환

모든 파일과 폴더는 파일 탐색기에 트리로 표시됩니다. 트리에서 파일을 클릭하면 서로 전환 할 수 있습니다.

## 파일 이름

탐색 줄에서 파일 이름을 클릭하거나 파일 탐색기에서 ** 이름 바꾸기 ** 버튼을 클릭하여 현재 파일의 이름 을 바꿀 수 있습니다 .

## 파일 삭제

파일 탐색기에서 ** 제거 ** 단추를 클릭하십시오. 파일이 ** 여전히 ** 폴더로 이동하고 7 일 동안 활동이 자동으로 삭제되었습니다.

## 파일 내보내기

You can export the current file by clicking **Export to disk** in the menu. You can choose to export the file as plain Markdown, as HTML using a Handlebars template or as a PDF.


# Synchronization

Synchronization is one of the biggest features of StackEdit. It enables you to synchronize any file in your workspace with other files stored in your **Google Drive**, your **Dropbox** and your **GitHub** accounts. This allows you to keep writing on other devices, collaborate with people you share the file with, integrate easily into your workflow... The synchronization mechanism takes place every minute in the background, downloading, merging, and uploading file modifications.

There are two types of synchronization and they can complement each other:

- The workspace synchronization will sync all your files, folders and settings automatically. This will allow you to fetch your workspace on any other device.
	> To start syncing your workspace, just sign in with Google in the menu.

- The file synchronization will keep one file of the workspace synced with one or multiple files in **Google Drive**, **Dropbox** or **GitHub**.
	> Before starting to sync files, you must link an account in the **Synchronize** sub-menu.

## Open a file

You can open a file from **Google Drive**, **Dropbox** or **GitHub** by opening the **Synchronize** sub-menu and clicking **Open from**. Once opened in the workspace, any modification in the file will be automatically synced.

## Save a file

You can save any file of the workspace to **Google Drive**, **Dropbox** or **GitHub** by opening the **Synchronize** sub-menu and clicking **Save on**. Even if a file in the workspace is already synced, you can save it to another location. StackEdit can sync one file with multiple locations and accounts.

## Synchronize a file

Once your file is linked to a synchronized location, StackEdit will periodically synchronize it by downloading/uploading any modification. A merge will be performed if necessary and conflicts will be resolved.

If you just have modified your file and you want to force syncing, click the **Synchronize now** button in the navigation bar.

> **Note:** The **Synchronize now** button is disabled if you have no file to synchronize.

## Manage file synchronization

Since one file can be synced with multiple locations, you can list and manage synchronized locations by clicking **File synchronization** in the **Synchronize** sub-menu. This allows you to list and remove synchronized locations that are linked to your file.


# Publication

Publishing in StackEdit makes it simple for you to publish online your files. Once you're happy with a file, you can publish it to different hosting platforms like **Blogger**, **Dropbox**, **Gist**, **GitHub**, **Google Drive**, **WordPress** and **Zendesk**. With [Handlebars templates](http://handlebarsjs.com/), you have full control over what you export.

> Before starting to publish, you must link an account in the **Publish** sub-menu.

## Publish a File

You can publish your file by opening the **Publish** sub-menu and by clicking **Publish to**. For some locations, you can choose between the following formats:

- Markdown: publish the Markdown text on a website that can interpret it (**GitHub** for instance),
- HTML: publish the file converted to HTML via a Handlebars template (on a blog for example).

## Update a publication

After publishing, StackEdit keeps your file linked to that publication which makes it easy for you to re-publish it. Once you have modified your file and you want to update your publication, click on the **Publish now** button in the navigation bar.

> **Note:** The **Publish now** button is disabled if your file has not been published yet.

## Manage file publication

Since one file can be published to multiple locations, you can list and manage publish locations by clicking **File publication** in the **Publish** sub-menu. This allows you to list and remove publication locations that are linked to your file.


# Markdown extensions

StackEdit extends the standard Markdown syntax by adding extra **Markdown extensions**, providing you with some nice features.

> **ProTip:** You can disable any **Markdown extension** in the **File properties** dialog.


## SmartyPants

SmartyPants converts ASCII punctuation characters into "smart" typographic punctuation HTML entities. For example:

|                |ASCII                          |HTML                         |
|----------------|-------------------------------|-----------------------------|
|Single backticks|`'Isn't this fun?'`            |'Isn't this fun?'            |
|Quotes          |`"Isn't this fun?"`            |"Isn't this fun?"            |
|Dashes          |`-- is en-dash, --- is em-dash`|-- is en-dash, --- is em-dash|


## KaTeX

You can render LaTeX mathematical expressions using [KaTeX](https://khan.github.io/KaTeX/):

The *Gamma function* satisfying $\Gamma(n) = (n-1)!\quad\forall n\in\mathbb N$ is via the Euler integral

$$
\Gamma(z) = \int_0^\infty t^{z-1}e^{-t}dt\,.
$$

> You can find more information about **LaTeX** mathematical expressions [here](http://meta.math.stackexchange.com/questions/5020/mathjax-basic-tutorial-and-quick-reference).


## UML diagrams

You can render UML diagrams using [Mermaid](https://mermaidjs.github.io/). For example, this will produce a sequence diagram:

``` 머메이드 
시퀀스 
다이어그램 앨리스->> 밥 : 안녕하세요 밥, 잘 지내? 
밥->> 존 : 요한은 어때요? 
Bob--x Alice : 감사합니다. 
Bob-x John : 감사합니다. 
John의 오른쪽 참고 : Bob은 텍스트가 행에 맞지 않을 정도로 긴 시간, 긴 시간을 생각합니다. Bob- > 앨리스 : John과 확인 중 ... Alice-> John : 예 ... John, 잘 지내시나요? ```





그리고 이것은 순서도를 생성합니다 :

`` 어 
그래프 LR 
A [사각형 스퀘어] - 링크 텍스트 -> B ((원)) 
A -> C (둥근 사각형) 
B -> {D} 마름모 
C -> D ```

<!--stackedit_data:
eyJoaXN0b3J5IjpbNjY4NjI5MTQ4XX0=
-->