
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
            ```
            ```
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

### `RVX player widget`
### Import
##### Native JS usage:

Import ava-widgets-sdk.js / https://salmon-mushroom-072389f0f.azurestaticapps.net/scripts.js to your HTML file:
```html live
    <head>
        <script async type=”module” src="./ava-widgets-sdk.js"></script>
    </head>
```

```html live
   <head>
        <script async type=”module” src="https://salmon-mushroom-072389f0f.azurestaticapps.net/scripts.js"></script>
   </head>
```

##### Typescript usage:

``` 
import { RVXWidget } from '@video-analytics/widgets';
```

### Getting Started
RVX widget is a web-component that can be created using HTML or dynamically. 

Creating using HTML:
```html live
  <head>
	…
 	..
  <body>
	<rvx-widget><rvx-widget>
  </body>
```

Creating dynamically:

##### Native JS usage:
```html live
  <head>
    <script async type=”module” src="https://salmon-mushroom-072389f0f.azurestaticapps.net/scripts.js"></script>
  </head>
  <body>
	…
  </body>
  <script>(function () {
            const rvxWidget = new window.ava.widgets.rvx();
            document.firstElementChild.appendChild(rvxWidget)
  })()
</script>
```

##### Typescript usage:
``` 
import { RVXWidget } from '@video-analytics/widgets';

const rvxWidget = new RVXWidget();
document.firstElementChild.appendChild(RVXWidget).
```

### Properties
Name | Type | Default | Description 
------------ | ------------- | ------------- | -------------
width	| string	         | 100%	| Reflects the value of widget width.
height	| string	         | 100%	| Reflects the value of widget height
config	| IRVXWidgetConfig	 | null	| Widget configuration

### Events
Name | Parameters | Description 
------------ | ------------- | -------------
TOKEN_EXPIRED	| -	         | Callback to invoke when AVA JWT token is expired.

### Methods
Name | Parameters | Description 
------------ | ------------- | -------------
constructor 	| width: string = '', height: string = '', config: IRVXWidgetConfig = null	| Widget constructor. If called with config, you don’t need to call _configure_ function
setAccessToken	| jwtToken:string	| Update the widget token. 
set apiBase	    | apiBase:string	| Control AVA-API base. Good for using mock API / testing API.
configure	    | config: IRVXWidgetConfig	| Update widget configuration.
load	        | -	                | Loads and initialize the widget according to provided configuration. If not called, widget will be empty  


### Code snippets:

1.  *Basic usage snippet:* create an RVX widget with native JS code, configure the widget and load the data.
    ```html live
        <head>
            <script async type=”module” src="https://salmon-mushroom-072389f0f.azurestaticapps.net/scripts.js"></script>
        </head>
        <body>  
            <rvx-widget></rvx-widget>
        </body>
        <script>(function () {
            // Get RVX instance 
            const rvxWidget = document.querySelector("rvx-widget");
            
            // Configure rvx widget with AVA API configuration
            rvxWidget.configure({
                token: '<AVA-API-JWT-TOKEN>',
                accountId: '<GUID-ACCOUNT-ID>’,
                longRegionCode: '<REGION-CODE>',
                videoName: '<VIDEO-NAME-FROM-AVA-ACCOUNT>’
            });

            rvxWidget.load();
        })()
        </script>
    ```

2.  *Token refresh snippet:* create an RVX widget with native JS code, configure the widget and load the data. Once AVA-API token is expired, update the token.
    ```html live
        <head>
            <script async type=”module” src="https://salmon-mushroom-072389f0f.azurestaticapps.net/scripts.js"></script>
        </head>
        <body>  
            <rvx-widget widget=”920px” height=”300px”></rvx-widget>
        </body>
        <script>(function () {
                // Get RVX instance 
                const rvxWidget = document.querySelector("rvx-widget");

                // Adding token expired listener
                rvxWidget.addEventListener('TOKEN_EXPIRED', async () => {
                    const token = await fetch(‘<request-to-generate-token>’);
                    rvxWidget.setAccessToken(token);
                });

                // Configure rvx widget with AVA API configuration
                rvxWidget.configure({
                    token: '<AVA-API-JWT-TOKEN>',
                    accountId: '<GUID-ACCOUNT-ID>’,
                    longRegionCode: '<REGION-CODE>',
                    videoName: '<VIDEO-NAME-FROM-AVA-ACCOUNT>’
                });

                // Load the widget
                rvxWidget.load();
        })()
        </script>
    ```

3.  *Dynamically creating the widget:* create an RVX widget dynamically with native JS code, without using configure function.
    ```html live
            <head>
                <script async type=”module” src="https://salmon-mushroom-072389f0f.azurestaticapps.net/scripts.js"></script>
                </head>
            <body>  
                <div id=”widget-container”></div>
            </body>
            <script>(function () {
                    // Get widget container 
                    const widgetContainer = document.querySelector("#widget-container");

                    // Create new RVX widget
                    const rvxWidget = new window.ava.widgets.rvx(
                    '100%',
                    '100%',
                    {
                                token: '<AVA-API-JWT-TOKEN>',
                                accountId: '<GUID-ACCOUNT-ID>’,
                                longRegionCode: '<REGION-CODE>',
                                videoName: '<VIDEO-NAME-FROM-AVA-ACCOUNT>’
                    });

                    widgetContainer.appendChild(rvxWidget)

                    // Load the widget
                    rvxWidget.load();
            })()
            </script>
    ```

4.  *Use rvx-widget in your angular application:*

    1.	Go to your _src/main.ts_ file and add the following code:
        ```
            import { RVXWidget } from '@media-video-analytics/widgets';

            /*
            * Ensure that tree-shaking doesn't remove this component from * the bundle. 
            * There are multiple ways to prevent tree shaking, of which this * is one.
            */
            RVXWidget;
        ```

    2.	To allow an NgModule to contain Non-Angular element names, add the following code in your application module typescript file _app.module.ts_:
        ```
            import { CUSTOM_ELEMENTS_SCHEMA } from '@angular/core';

            @NgModule({
            schemas: [CUSTOM_ELEMENTS_SCHEMA]
            })
        ```

    3.	Now we can start using RVX widget. Replace the HTML template in your app.component.html, file with the following markup:
        ```html live
            <template>
                <rvx-widget></rvx-widget>
            </template>
        ```
        Alternatively, you can create a new instance of RVX-Widget using typescript, and add it to the DOM.
