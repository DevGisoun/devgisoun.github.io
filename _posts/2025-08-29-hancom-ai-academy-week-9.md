---
title: "[스나이퍼팩토리] 한컴AI 2기 - 교육 9주차 후기"
description: >-
  Node.js Express 환경에서 PUG와 Sequelize를 이용한 사용자 관리 시스템 구축부터, SSE, WebSocket, Socket.IO를 활용한 실시간 채팅 및 동시편집 협업 도구(텍스트 에디터, 화이트보드) 개발 과정 기술.
author: gisoun
date: 2025-08-29 09:28:00 +0900
categories: [Hancom AI Academy, Education]
tags: [hancom, hancom ai academy, education, ai, nodejs, express, pug, seuquelize, orm, database, mongodb, sse, websocket, socketio]
pin: false
media_subpath: '/assets/posts/20250829'
published: true
---

> 2025\. 8\. 25\. ~ 2025\. 8\. 29\.

---

## 개요

이번 주차에는 **Node.js** 의 **Express** 프레임워크를 기반으로 다양한 웹 애플리케이션을 구축하는 실습을 진행했습니다.  

이번 포스팅에서는 **PUG** 와 **Sequelize ORM** 을 활용한 사용자 관리 시스템 개발 경험과, **SSE**, **WebSocket**, **Socket.IO** 와 같은 실시간 통신 기술을 적용하여 만든 **실시간 채팅** 및 **동시편집 협업 도구(텍스트 에디터, 화이트보드)** 프로젝트에 대해 다룹니다. 각 기술의 핵심 개념과 코드 예시를 통해 학습 과정을 상세히 기술하도록 하겠습니다.

---

## 사용자 관리 시스템 (PUG 템플릿 적용)

먼저, **PUG** 템플릿 엔진을 사용하여 동적인 웹 페이지를 구현했습니다. **PUG**는 **HTML**의 정적인 단점을 개선하기 위한 템플릿 엔진으로, 변수, 조건문, 반복문 같은 프로그래밍 요소를 활용해 동적인 **HTML** 페이지를 생성할 수 있게 해줍니다.  

**PUG**의 가장 큰 특징은 **Ruby**와 유사한 간결한 문법입니다. 들여쓰기를 통해 태그의 계층 구조를 표현하며, 괄호나 닫는 태그를 사용하지 않아 코드의 양이 크게 줄어듭니다.  

> 그러나 오히려 기존 **HTML** 문법과는 차이가 커서 호불호가 갈릴 수 있습니다.  
> **전 불호..**
{: .prompt-warning }

### PUG 핵심 문법 예시

1. **`변수 사용`**
   
   **Express** 라우터에서 

   **`res.render('index', { title: 'Express' });`** 와 같이 변수를 전달하면 , **PUG** 파일 내에서 

   **`#{}`** 또는 **`=`** 를 사용해 해당 변수를 렌더링할 수 있습니다.

   ```
   //- routes/index.js 에서 { title: 'Express' } 전달
   h1= title
   p Welcome to #{title}
   ```

   위 코드는 아래와 같은 **HTML**로 변환됩니다.

   ```html
   <h1>Express</h1>
   <p>Welcome to Express</p>   
   ```

2. 반복문

   **`each ... in ...`** 문법을 사용하여 배열이나 객체를 순회하며 **HTML** 요소를 반복 생성할 수 있습니다.

   ```
   ul
     each fruit in ['사과', '배', '오렌지']
       li= fruit   
   ```

   위 코드는 아래와 같은 **HTML** **`<ul>`** 리스트를 만듭니다.

   ```html
   <ul>
     <li>사과</li>
     <li>배</li>
     <li>오렌지</li>
   </ul>   
   ```

이러한 **PUG**의 기능을 활용하여 사용자 목록을 동적으로 생성하고, 사용자 등록 폼을 만드는 등의 기능을 구현했습니다.

![image](pug-001.png)
_PUG 템블릿 기반 사용자 관리 시스템_

---

## 사용자 관리 시스템 (Sequelize ORM 활용)

다음 실습은 **Sequelize** ORM을 학습하기 위한 별개의 사용자 관리 시스템을 구현하였습니다. 이번 실습에서는 **PUG**가 아닌 **Nunjucks**라는 템플릿 엔진을 사용하여 화면을 구성했습니다.

**Nunjucks**는 JavaScript 기반 템플릿 엔진으로, **PUG**와는 분명한 차이점이 있습니다. **PUG가 들여쓰기 기반의 간결한 문법으로 HTML 태그 자체를 대체**하는 반면, **Nunjucks는 기존 HTML 구조를 그대로 유지하면서 `{% raw %}{{ 변수 }}{% endraw %}`나 `{% raw %}{% 제어문 %}{% endraw %}` 같은 특별한 문법을 삽입하여 동적인 부분을 처리**합니다. 이 덕분에 **HTML**에 익숙한 저로서는 더 쉽게 적응할 수 있다는 장점이 있었습니다.

해당 실습의 핵심 목표는 **SQL** 쿼리 없이 **Javascript** 코드로 데이터베이스를 다루는 **ORM**의 개념을 익히는 것이었습니다.

**Sequelize**를 사용하면 다음과 같은 장점이 있습니다.

- **`생산성 향상`**: 복잡한 **SQL** 문을 직접 작성하지 않아도 되므로 개발 속도가 빨라집니다!
- **`코드 가독성`**: Javascript 문법으로 데이터베이스 로직을 작성하여 코드를 더 쉽게 이해할 수 있습니다.  
   > 다만, **Sequelize** 같은 **ORM**이 자동으로 **SQL**을 생성해주는 과정은 개발자가 직접 쿼리를 작성할 기회가 줄어들어 **SQL 숙련도가 낮아질 수 있습니다.**
   >
   > 또한, **ORM**이 제공하는 문법의 한계로 인해, 여러 테이블을 조인하거나 특정 데이터베이스의 고급 기능을 사용하는 **복잡한 쿼리는 작성하기가 더 까다로울 수 있습니다.**
   {: .prompt-warning }
- **`데이터베이스 호환성`**: 실습에서 사용한 **MySQL** 뿐만 아니라 **PostgreSQL**, **MSSQL** 등 다양한 **관계형 데이터베이스(RDB)**와 호환되어 데이터베이스 전환이 용이합니다.

### Sequelize 핵심 쿼리 예시

1. **`데이터 생성 (Create)`**
   
   **SQL** 의 **`INSERT`** 문은 **`User.create()`** 메서드로 대체됩니다.
   ```javascript
   // SQL
   // INSERT INTO users (name, age, married) VALUES ('김철수', 25, false);
   
   // Sequelize
   const { User } = require('../models');

   await User.create({
     name: '기순',
     age: 28,
     married: false,
   });
   ```

2. **`데이터 조회 (Read)`**

   **SQL** 의 **`SELECT ... WHERE`** 절은 **`findAll({ where: ... })`** 과 같이 객체 형태로 표현됩니다.

   ```javascript
   // SQL
   // SELECT name, age FROM users WHERE married = 1 AND age > 30;
   
   // Sequelize
   const { Op } = require('sequelize');
   const { User } = require('../models');
   
   await User.findAll({
     attributes: ['name', 'age'],
     where: {
       married: 1,
       age: { [Op.gt]: 22 }, // age > 22
     },
   });
   ```

3. **`데이터 수정 (Update) 및 삭제 (Delete)`**

   **`UPDATE`**와 **`DELETE`** 역시 각각 **`User.update()`**와 **`User.destroy()`** 메서드로 간단하게 처리할 수 있습니다.

   실제 **Express** 라우터에서는 아래와 같이 **Sequelize** 메서드를 사용하여 비동기 로직을 처리합니다.

   ```javascript
   // routes/users.js
   
   const express = require('express');
   const User = require('../models/user'); // Sequelize 모델 가져오기
   const router = express.Router();
   
   // 모든 사용자 조회
   router.get('/', async (req, res, next) => {
     try {
       const users = await User.findAll();
       res.render('user', { users }); // 조회된 사용자를 템플릿에 전달하여 렌더링
     } catch (err) {
       console.error(err);
       next(err);
     }
   });
   
   // 사용자 등록
   router.post('/', async (req, res, next) => {
     try {
       await User.create({
         name: req.body.name,
         age: parseInt(req.body.age),
         married: req.body.married === 'on',
       });
       res.redirect('/users'); // 등록 후 목록 페이지로 Redirect
     } catch (err) {
       console.error(err);
       next(err);
     }
   });
   
   module.exports = router;
   ```

**Sequelize** 를 통해 **SQL** 쿼리가 **Javascript** 코드로 통합되면서, 전체적인 코드 구조가 더 깔끔하고 직관적으로 변경되었습니다.

![image](sequelize-001.png)
_Sequelize 를 적용한 최종 실행 결과 화면_

---

## SSE 예제 - 카운트 다운

이번에는 **SSE(Server-Sent Events)** 기술을 사용하여 서버에서 클라이언트로 데이터를 실시간으로 푸시하는 예제를 다뤄보았습니다.  

**SSE**는 **서버에서 클라이언트로만 데이터 전송이 가능한 단방향 통신 기술**입니다. 과거에 사용되던 **폴링(Polling)** 방식은 클라이언트가 주기적으로 서버에 업데이트가 있는지 물어봐야 했지만, **SSE**는 최초 연결 후 서버가 필요할 때마다 클라이언트에 데이터를 직접 보내줄 수 있어 훨씬 효율적입니다.

**Express** 서버에서 **SSE**를 구현하기 위해서는 먼저 **HTTP 헤더**를 특정 방식으로 설정해야 합니다. 그 후 **`setInterval`** 같은 함수를 이용해 주기적으로 클라이언트에 데이터를 전송합니다.

```javascript
// SSE 엔드포인트
app.get('/events', (req, res) => {
  // SSE 를 위한 헤더 설정
  res.setHeader('Content-Type', 'text/event-stream');
  res.setHeader('Cache-Control', 'no-cache');
  res.setHeader('Connection', 'keep-alive');

  // 최초 연결 시 메시지 전송
  res.write('data: {"message": "연결되었습니다"}\\n\\n');

  // 1초마다 현재 시간을 데이터로 전송
  const intervalId = setInterval(() => {
    const data = { time: new Date().toLocaleTimeString() };

    // 'update' 라는 이벤트 타입으로 데이터 전송
    res.write("event: update\\n");
    res.write(`data: ${JSON.stringify(data)}\\n\\n`);
  }, 1000);

  // 클라이언트 연결 종료 시 Interval 정리
  req.on('close', () => {
    clearInterval(intervalId);
    console.log('클라이언트 연결 종료');
  });
});
```

클라이언트에서는 이 데이터를 받아 실시간으로 화면에 현재 서버 시간을 표시하게 됩니다.

![image](timer-001.png)
_실시간으로 화면에 표시되는 현재 서버 시간_

---

## WebSocket 기반 실시간 채팅

다음으로 **WebSocket** 을 이용해 실시간 양방향 채팅 애플리케이션을 만들어보았습니다. **WebSocket**은 **SSE**와 달리 **클라이언트와 서버가 서로 자유롭게 데이터를 주고받을 수 있는 양방향 통신 기술**입니다. 

**`ws`** 프로토콜을 사용하며, 한 번 연결이 수립되면 그 연결을 통해 계속해서 데이터를 교환하므로 매우 빠르고 효율적입니다.

**WebSocket** 서버는 기존의 HTTP 서버에 연결(attach)하여 동일한 포트를 공유할 수 있습니다.

```javascript
// Express 로 HTTP 서버 생성
const app = express();
const server = http.createServer(app);

// WebSocket 서버를 HTTP 서버에 연결
const wss = new WebSocket.Server({ server });

// 클라이언트 연결 이벤트 처리
wss.on('connection', (ws) => {
  // 새로운 클라이언트가 보낸 메시지 처리
  ws.on('message', (message) => {
    // 받은 메시지를 모든 클라이언트에게 전송 (브로드캐스트)
    wss.clients.forEach((client) => {
      if (client.readyState === WebSocket.OPEN) {
        client.send(message.toString());
      }
    });
  });

  // 연결 종료 이벤트 처리
  ws.on('close', () => {
    console.log('클라이언트 연결 종료');
  });
});
```

이 코드는 특정 클라이언트로부터 메시지를 받으면, 현재 연결된 모든 클라이언트에게 해당 메시지를 그대로 다시 보내는 간단한 브로드캐스트 방식의 채팅 로직을 구현한 것입니다.

![image](ws-chat-001.png)
_서로 다른 브라우저에서 테스트한 양방향 채팅 화면_

---

## Socket.io 기반 실시간 채팅 (using. MongoDB)

다음으로 **Socket.IO** 라이브러리와 **MongoDB** 를 결합하여 기능이 더 확장된 **GIF 채팅방** 기능을 구현하였습니다. **Socket.IO**는 **WebSocket** 한 단계 더 추상화하여 개발을 편리하게 해주는 라이브러리입니다. **Node.js**의 기본 **`http`** 모듈보다 **Express** 프레임워크를 사용하는 것이 더 편리한 것과 비슷한 거 같네요.  

이번 실습은 이전 **WebSocket 채팅**과 달리, **MongoDB** 를 사용하여 채팅 내용과 채팅방 정보를 영구적으로 저장하는 기능을 추가했습니다. 또한, **Socket.IO** 의 **'Namespace'**와 **'Room'** 개념을 활용하여 채팅 로직을 체계적으로 분리했습니다.  

- **`네임스페이스(Namespace)`**: **Socket.IO** 연결을 위한 별도의 채널입니다. 예를 들어  
   **`/room`** 네임스페이스는 방 목록 관리를, **`/chat`** 네임스페이스는 실제 채팅을 담당하도록 분리할 수 있습니다.  
- **`방(Room)`**: 네임스페이스 내에서 특정 클라이언트들끼리만 통신할 수 있는 논리적인 공간입니다.  
   **`socket.join(방_아이디)`**로 방에 입장하고, **`io.to(방_아이디).emit(...)`** 으로 특정 방에만 메시지를 보낼 수 있습니다.

**채팅 메시지 처리 핵심 코드**
```javascript
// 채팅 메시지를 DB에 저장하고 해당 방에 전송하는 라우터
exports.sendChat = async (req, res, next) => {
  try {
    // Mongoose 모델을 사용해 채팅 내용을 DB에 저장
    const chat = await Chat.create({
      room: req.params.id,
      user: req.session.color,
      chat: req.body.chat,
    });

    // Socket.IO를 통해 해당 방(room)에만 'chat' 이벤트를 보냄
    req.app.get('io').of('/chat').to(req.params.id).emit('chat', chat);
    res.send('ok');
  } catch (error) {
    console.error(error);
    next(error);
  }
};
```

이처럼 **Socket.IO**와 데이터베이스를 연동하여, 단순히 실시간 메시지를 주고받는 것을 넘어 영속성 있는 채팅 애플리케이션을 구현할 수 있었습니다.

![image](chat-room-001.png)
_MongoDB 와 연동되어 보여지는 채팅방 리스트_

![image](chat-room-002.png)
_서로 다른 브라우저에서 테스트한 양방향 채팅 화면_

---

## 동시편집

**WebSocket** 의 실시간 양방향 통신 기능을 활용하면 여러 사용자가 동시에 문서를 편집하거나 그림을 그리는 등 협업 도구를 만들 수 있습니다.

### 텍스트 에디터

이 실습의 목표는 여러 사용자가 하나의 **텍스트 입력창(textarea)**에 동시에 글을 쓸 때, 모든 사용자의 화면에 해당 내용이 실시간으로 동기화되는 것입니다.

#### 핵심 서버 코드

서버는 특정 클라이언트로부터 메시지를 받으면, 메시지를 보낸 당사자를 제외한 다른 모든 클라이언트에게만 해당 메시지를 브로드캐스트합니다. 이는 메시지를 보낸 클라이언트의 입력창에 내용이 중복으로 입력되는 것을 방지하기 위함입니다.  

```javascript
// server.js
const express = require('express');
const http = require('http');
const path = require('path');
const WebSocket = require('ws');

const app = express();
app.use(express.static(path.join(__dirname, 'public')));
const server = http.createServer(app);
const wss = new WebSocket.Server({ server });

// WebSocket 연결 이벤트 처리
wss.on('connection', (ws) => {
  console.log('New client connected.');

  // 클라이언트로부터 메시지를 받았을 때의 이벤트 처리
  ws.on('message', (message) => {
    const receivedMessage = message.toString();

    // 받은 메시지를 보낸 클라이언트를 제외한 모든 클라이언트에게 브로드캐스트
    wss.clients.forEach((client) => {
      if (client !== ws && client.readyState === WebSocket.OPEN) {
        client.send(receivedMessage);
      }
    });
  });

  ws.on('close', () => {
    console.log('Client disconnected.');
  });
});

const PORT = process.env.PORT || 8091;
server.listen(PORT, () => {
    console.log(`Server is listening on port ${PORT}.`);
});
```

#### 핵심 클라이언트 코드

클라이언트는 텍스트 입력창에 변화가 생길 때마다 현재 텍스트 전체를 서버로 보냅니다. 서버로부터 메시지를 받으면 텍스트 입력창의 내용을 해당 메시지로 덮어쓰는데, 이때 다른 사람의 입력으로 인해 자신의 커서(cursor) 위치가 멋대로 맨 뒤로 이동하는 것을 방지하기 위해 커서 위치를 보정하는 로직을 별도로 추가하였습니다.

```html
<script>
    const protocol = window.location.protocol === 'https:' ? 'wss:' : 'ws:';
    const socket = new WebSocket(`${protocol}//${window.location.host}`);
    const editor = document.getElementById('editor');

    // 서버로부터 메시지 수신
    socket.onmessage = (event) => {
        // 다른 클라이언트의 입력으로 인해 커서 위치가 맨 뒤로 가는 것을 방지
        const currentCursorPosition = editor.selectionStart;
        const originalLength = editor.value.length;
            
        editor.value = event.data;
            
        const newLength = editor.value.length;
        const lengthDifference = newLength - originalLength;

        // 텍스트 변경 후 커서 위치 조정
        editor.selectionStart = currentCursorPosition + lengthDifference;
        editor.selectionEnd = currentCursorPosition + lengthDifference;
    };

    // 텍스트 에디터에 입력 시 서버에 전송
    editor.addEventListener('input', () => {
        if (socket.readyState === WebSocket.OPEN) {
            socket.send(editor.value);
        }
    });
</script>
```

![image](ws-text-editor-001.png)
_동시 편집 텍스트 에디터_

### 화이트보드

텍스트 에디터에 이어, 이번에는 여러 사용자가 동시에 그림을 그릴 수 있는 실시간 협업 화이트보드를 구현해보았습니다. 텍스트 대신 **캔버스** 좌표 데이터를 주고받는다는 점을 제외하면 원리는 텍스트 에디터와 동일합니다.

사용자가 캔버스에 마우스를 드래그하여 선을 그리면, **`mousemove`** 이벤트가 발생할 때마다 시작 좌표와 끝 좌표 데이터가 JSON 형식으로 서버에 전송됩니다. 서버는 이 데이터를 받아 다른 모든 클라이언트에게 브로드캐스트하고, 클라이언트들은 수신한 좌표 데이터를 이용해 자신의 캔버스에 동일한 선을 그리게 됩니다.

#### 핵심 서버 코드

서버의 역할은 텍스트 에디터 예제와 거의 동일합니다. 그림 좌표 데이터가 담긴 메시지를 받으면, 보낸 사람을 제외한 모든 클라이언트에게 전달합니다.

```javascript
// server.js

// ...

const wss = new WebSocket.Server({ server });

wss.on('connection', (ws) => {
  console.log('New client connected.');

  ws.on('message', (message) => {
    // 받은 메시지를 보낸 클라이언트를 제외하고, 다른 클라이언트에게만 메시지 전송
    wss.clients.forEach((client) => {
      if (client !== ws && client.readyState === WebSocket.OPEN) {
        client.send(message.toString());
      }
    });
  });

  ws.on('close', () => {
    console.log('Disconnected client.');
  });
});

// ...
```

#### 핵심 클라이언트 코드

클라이언트는 캔버스 위에서 발생하는 마우스 이벤트(**`mousedown`**, **`mousemove`**, **`mouseup`**)를 감지하여 그림을 그리는 로직을 처리합니다. **`mousemove`** 이벤트가 발생할 때마다 자신의 캔버스에 선을 그림과 동시에, 해당 좌표 정보를 **WebSocket** 을 통해 서버로 전송합니다. 또한, 서버로부터 다른 사용자의 그림 데이터를 받으면, 그 데이터로 자신의 캔버스에 선을 그려 동기화합니다.

```html
<canvas id="whiteboard" width="800" height="600"></canvas>
<script>
    const canvas = document.getElementById('whiteboard');
    const ctx = canvas.getContext('2d');

    // WebSocket 연결 설정
    const protocol = window.location.protocol === 'https:' ? 'wss:' : 'ws:';
    const socket = new WebSocket(`${protocol}//${window.location.host}`);

    let isDrawing = false;
    let lastX = 0, lastY = 0;

    function draw(x0, y0, x1, y1) {
        ctx.beginPath();
        ctx.moveTo(x0, y0);
        ctx.lineTo(x1, y1);
        ctx.stroke();
    }

    // 마우스 드래그 시 로컬 캔버스에 그리고, 서버로 데이터 전송
    canvas.addEventListener('mousemove', (e) => {
        if (!isDrawing) return;
        const [currentX, currentY] = [e.offsetX, e.offsetY];
        draw(lastX, lastY, currentX, currentY); // 내 캔버스에 그리기
        const drawingData = { x0: lastX, y0: lastY, x1: currentX, y1: currentY };
        socket.send(JSON.stringify(drawingData)); // 서버로 전송
        [lastX, lastY] = [currentX, currentY];
    });
    
    // ... (mousedown, mouseup 이벤트 리스너)
    // 다른 사용자의 그림 데이터 수신 시 내 캔버스에 그리기
    socket.onmessage = (event) => {
        const data = JSON.parse(event.data);
        draw(data.x0, data.y0, data.x1, data.y1);
    };
</script>
```

이 예제를 통해 **WebSocket** 을 활용하여 실시간 그래픽 협업 도구의 기본적인 형태를 구현해볼 수 있었습니다.

![image](ws-white-board-001.png)
_동시 편집 화이트보드 에디터_

---

## 마무리

이번 주차 교육을 통해 **Node.js** 와 **Express** 기반 웹 애플리케이션의 다양한 속성을 넓게 다룰 수 있었습니다. 단순히 데이터를 CRUD 하는 웹 서버를 넘어, **PUG**, **Nunjucks** 같은 템플릿 엔진으로 동적 UI 를 구성하고, **Sequelize ORM** 으로 데이터베이스를 효율적으로 관리하는 방법을 익혔습니다.  

특히 **SSE**, **WebSocket**, **Socket.IO** 를 학습하며 예전부터 직접 구현해보고 싶었던 **실시간(Realtime)** 기술의 중요성을 체감했습니다. 실시간 채팅방부터 동시편집 협업 도구까지 직접 구현해보면서, 단방향 통신과 양방향 통신의 차이를 명확히 이해하고 각 기술의 장단점과 적합한 사용 사례를 파악할 수 있었습니다.  

이번 주에 배운 내용들은 앞으로 더 복잡하고 상호작용이 풍부한 웹 서비스를 만드는 데 튼튼한 기반이 될 것이라 생각합니다.

---

본 후기는 [한글과컴퓨터x한국생산성본부x스나이퍼팩토리] 한컴 AI 아카데미 2기 (B-log) 리뷰로 작성 되었습니다.

#한컴AI아카데미2기 #AI개발자 #AI개발자교육 #한글과컴퓨터 #한국생산성본부 #스나이퍼팩토리 #부트캠프 #AI전문가양성 #개발자교육 #개발자취업
