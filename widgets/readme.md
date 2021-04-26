
![ava_widgets_banner_github.png](./ava_widgets_banner_github.png)

# Azure video analyzer widgets

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![TypeScript](https://img.shields.io/badge/%3C%2F%3E-TypeScript-%230074c1.svg)](https://www.typescriptlang.org/)
[![code style: prettier](https://img.shields.io/badge/code_style-prettier-f8bc45.svg)](https://github.com/prettier/prettier)

This is the Azure video analyzer widgets repo, containing web component packages, examples, and documentation.

## Introduction

A collection of widgets (web components) using Azure Video Analyzer platform capabilities and APIs

## Prerequisites
###### NOTE: this is relevant during development mode. After releasing to GITHUB, the flow will be updated.

1.	#### For consuming at runtime:
    In this option, you can **build the library yourself** or **import the build library from a blob**.
    _For building AVA widgets library_, please make sure you have access to the following repo - [AVA-Widgets](https://dev.azure.com/MediaWidgets/AVA%20Widgets)
    If not, please reach out to @Nofar Edan or @Ori Ziv to get access.

    _For importing the library from a blob_, please make sure you have access to the following file:  https://salmon-mushroom-072389f0f.azurestaticapps.net/scripts.js 

2.	#### For consuming as NPM package from Azure private feed: 
    Access to feed: please make sure you have access to [Media-AVA-Widgets](https://dev.azure.com/MediaWidgets/AVA%20Widgets/_packaging?_a=feed&feed=Media-AVA-Widgets) private feed: 

    Connect to Media-AVA-widgets feed:
    a.	Enter [Media-AVA-Widgets](https://dev.azure.com/MediaWidgets/AVA%20Widgets/_packaging?_a=feed&feed=Media-AVA-Widgets) 
    b.	Click on ‘Connect to feed’
    C.  Select 'npm'
    d.  Follow installation steps. 

## Installing AVA library
###### NOTE: this is relevant during development mode. After releasing to GITHUB, the flow will be updated.

1.	#### For consuming at runtime:
    _Build ava widgets library_-
        a.	Clone repo code: [AVA-Widgets](https://dev.azure.com/MediaWidgets/AVA%20Widgets)
        b.	Once cloned, enter repository location and write the following commands:
            ```
            npm install
            npm run build
            ```
            Once build is done, enter _/dist_ folder, there you will find _ava-widgets-sdk.js_ file.

    _For importing from a blob option, you can skip this step._

2.	#### For consuming as NPM package from Azure private feed: 
    a.  Create in your application an _.npmrc_ file and follow the steps in . [Prerequisites/2](/Prerequisites/2) 
    b.  Install the library:
        ```
            npm install @video-analyzer/widgets
        ```