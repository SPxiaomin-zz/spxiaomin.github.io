---
title: 宁皓-node.js 课程笔记
date: 2016-12-13 18:12:40
categories: ['技术', '前端技术']
tags: ['nodejs']
---

## Events

1. 使用事件: EventEmitter

        const EventEmitter = require('events');

        class Player extends EventEmitter {}

        var player = new Player();

        player.on('play', () => {
            console.log('正在播放');
        });

        player.emit('play');

2. 事件的参数

        const EventEmitter = require('events');

        class Player extends EventEmitter {}

        var player = new Player();

        player.on('play', (track) => {
            console.log(`正在播放: 《${track}》`);
        });

        player.emit('play', '再见理想');

3. 只执行一次的事件监听器

        const EventEmitter = require('events');

        class Player extends EventEmitter {}

        var player = new Player();

        player.once('play', (track) => {
            console.log(`正在播放: 《${track}》`);
        });

        player.emit('play', '再见理想');
        player.emit('play', '海阔天空');

## File System

1. 得到文件与目录的信息: stat

        const fs = require('fs');

        fs.stat('index.js', (error, stats) => {
            if (error) {
                console.log(error);
            } else {
                console.log(stats);
                console.log(`文件: ${stats.isFile()}`);
                console.log(`目录: ${stats.isDirectory()}`);
            }
        });

2. 创建一个目录: mkdir

        const fs = require('fs');

        fs.mkdir('logs', (error) => {
            if (error) {
                console.log(error);
            } else {
                console.log('成功创建目录: logs');
            }
        });

3. 创建文件并写入内容: writeFile, appendFile

        const fs = require('fs');

        fs.writeFile('logs/hello.log', '您好 ~ \n', (error) => {
            if (error) {
                console.log(error);
            } else {
                console.log('成功写入文件');
            }
        });

        fs.appendFile('logs/hello.log', 'hello ~ \n', (error) => {
            if (error) {
                console.log(error);
            } else {
                console.log('成功写入文件');
            }
        });

4. 读取文件里的内容: readFile

    如果不设置编码 `utf8` 或者调用 `toString` 方法，返回的数据是二进制格式的。

        // 设置编码
        const fs = require('fs');

        fs.readFile('logs/hello.log', 'utf8', (error, data) => {
            if (error) {
                console.log(error);
            } else {
                console.log(data);
            }
        });

        // 调用toString()方法
        const fs = require('fs');

        fs.readFile('logs/hello.log', (error, data) => {
            if (error) {
                console.log(error);
            } else {
                console.log(data.toString());
            }
        });

5. 列出目录里的东西: readdir

        const fs = require('fs');

        fs.readdir('logs', (error, files) => {
            if (error) {
                console.log(error);
            } else {
                console.log(files);
            }
        });

6. 重命名目录或文件

        fs.rename('logs/hello.log', 'logs/greeting.log', (error) => {
            if (error) {
                console.log(error);
            } else {
                console.log('重命名成功');
            }
        });

7. 删除目录与文件: rmdir, unlink

        const fs = require('fs');

        fs.readdirSync('logs').map((file) => {
            fs.unlink(`logs/${file}`, (error) => {
                if (error) {
                    console.log(error);
                } else {
                    console.log(`成功的删除了文件: ${file}`);
                }
            });
        });

        fs.rmdir('logs', (error) => {
            if (error) {
                console.log(error);
            } else {
                console.log('成功的删除了目录: logs');
            }
        });

## Stream

1. 读取文件流（即，一块一块的读入文件）

        const fs = require('fs');

        var fileReadStream = fs.createReadStream('data.json');

        var count = 0;

        fileReadStream.once('data', (chunk) => {
            console.log(chunk.toString());
        });

        fileReadStream.on('data', (chunk) => {
            console.log(`${++count} 接收到: ${chunk.length}`);
        });

2. 可读流的事件

        const fs = require('fs');

        var fileReadStream = fs.createReadStream('data.json');

        var count = 0;

        fileReadStream.on('data', (chunk) => {
            console.log(`${++count} 接收到: ${chunk.length}`);
        });

        fileReadStream.on('end', () => {
            console.log('--- 结束 ---');
        });

        fileReadStream.on('error', (error) => {
            console.log(error);
        });

3. 可写的文件流（即，一块一块的写出文件）

        const fs = require('fs');

        var fileReadStream = fs.createReadStream('data.json');
        var fileWriteStream = fs.createWriteStream('data-1.json');

        var count = 0;

        fileReadStream.on('data', (chunk) => {
            console.log(`${++count} 接收到: ${chunk.length}`);
            fileWriteStream.write(chunk);
        });

        fileReadStream.on('end', () => {
            console.log('--- 结束 ---');
        });

        fileReadStream.on('error', (error) => {
            console.log(error);
        });

4. pipe

        const fs = require('fs');

        var fileReadStream = fs.createReadStream('data.json');
        var fileWriteStream = fs.createWriteStream('data-1.json');

        fileReadStream.pipe(fileWriteStream);

5. 链式使用pipe

        const fs = require('fs');
        const zlib = require('zlib');

        var fileReadStream = fs.createReadStream('data.json');
        var fileWriteStream = fs.createWriteStream('data-1.json.gz');

        fileWriteStream.on('pipe', (source) => {
            console.log(source);
        });

        fileReadStream
            .pipe(zlib.createGzip())
            .pipe(fileWriteStream);

## HTTP

1. request

        const http = require('http');

        var options = {
            protocol: 'http:',
            hostname: 'api.douban.com',
            port: '80',
            method: 'GET',
            path: '/v2/movie/top250'
        };

        var request = http.request(options, (response) => {
            // console.log(response);
            console.log(response.statusCode);
            console.log(response.headers);

        });

        request.on('error', (error) => {
            console.log(error);
        });

        request.end();

2. 利用请求回来的数据

        const http = require('http');

        var options = {
            protocol: 'http:',
            hostname: 'api.douban.com',
            port: '80',
            method: 'GET',
            path: '/v2/movie/top250'
        };

        var responseData = '';

        var request = http.request(options, (response) => {
            // console.log(response);
            // console.log((response.statusCode));
            // console.log(response.headers);

            response.setEncoding('utf8');
            response.on('data', (chunk) => {
                responseData += chunk;
            });

            response.on('end', () => {
                JSON.parse(responseData).subjects.map((item) => {
                    console.log(item.title);
                });
            });
        });

        request.on('error', (error) => {
            console.log(error);
        });

        request.end();

3. 创建服务器

        const http = require('http');

        var server = http.createServer();

        server.on('request', (request, response) => {
            response.writeHead(200, {
                'Content-Type': 'text/html'
            });
            response.end(`<h1>hello ~</h1>`);
        });

        server.listen(8080);

END.
