# vscode-Extensions
# localtojson README

## Features

A extension for exporting localStorage to JSON file

## Usage

1.Install the extension.


2.Add the following code to your HTML file's script tag or a JavaScript file:



3.Right-click on your target JSON file (where you want to save the exported data) in the VSCode Explorer.


4.Select the command localtojson.exportLocalStorage.


5.A message will appear indicating that the server is listening on port 3000.


6.Open the HTML file in your browser and execute the exportLocalStorage() function (manually or automatically).


7.After successful export, check your target JSON file.


1.将插件安装到本地.


2.将下列代码添加到script标签内或者一个js文件内（建议封装成函数，便于在需要的时候调用即可）.


3.在你的资源文件中选择你要把导出的JSON数据存储到的json文件（右键点击）'localtojson.exportLocalStorage'


4.如果成功，会提示3000端口已被监听，接下来打开一个html页面（包含下列js代码的页面）就可以导出该页面的localStorage了。





    ```javascript
        const localStorageData = {};
        for (let i = 0; i < localStorage.length; i++) {
            const key = localStorage.key(i);
            const value = localStorage.getItem(key);
            try {
                // 尝试将字符串解析为 JSON 对象
                localStorageData[key] = JSON.parse(value);
            } catch (error) {
                // 解析失败时保留原始字符串（例如非 JSON 值）
                localStorageData[key] = value;
            }
        }
        const jsonData = JSON.stringify(localStorageData, null, 2);

        try {
            const response = await fetch('http://localhost:3000/export', {
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json'
                },
                body: jsonData
            });
            if (response.ok) {
                alert('LocalStorage data exported successfully!');
            } else {
                alert('Failed to export LocalStorage data.');
            }
        } catch (error) {
            console.error('Error:', error);
            alert('An error occurred while exporting data.');
        }
    ```

