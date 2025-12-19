<!-- 情侣照片记录网页（Cloudflare Pages + Workers 方案） -->
<!-- 前端：Cloudflare Pages 静态站点 -->
<!-- 后端：Cloudflare Workers + KV / R2（示例以 KV 存元数据，R2 存图片） -->

<!DOCTYPE html>
<html lang="zh-CN">
<head>
  <meta charset="UTF-8" />
  <title>Love Memory · 美好生活记录</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <style>
    body {
      margin: 0;
      font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto;
      background: linear-gradient(135deg, #ff9a9e, #fad0c4);
      min-height: 100vh;
    }
    header {
      text-align: center;
      padding: 20px;
      color: #fff;
      font-size: 24px;
      font-weight: bold;
    }
    .card {
      background: #fff;
      max-width: 420px;
      margin: 20px auto;
      border-radius: 16px;
      box-shadow: 0 10px 30px rgba(0,0,0,0.15);
      padding: 20px;
    }
    input, button {
      width: 100%;
      padding: 12px;
      margin: 8px 0;
      border-radius: 8px;
      border: 1px solid #ddd;
      font-size: 16px;
    }
    button {
      background: #ff758c;
      border: none;
      color: #fff;
      cursor: pointer;
    }
    button:hover { opacity: 0.9; }
    .gallery {
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(140px, 1fr));
      gap: 10px;
      margin-top: 20px;
    }
    .gallery img {
      width: 100%;
      border-radius: 12px;
      object-fit: cover;
    }
  </style>
</head>
<body>

<header>💖 Love Memory</header>

<div class="card" id="loginCard">
  <h3>情侣登录</h3>
  <input id="username" placeholder="用户名" />
  <input id="password" type="password" placeholder="密码" />
  <button onclick="login()">登录 / 注册</button>
</div>

<div class="card" id="appCard" style="display:none;">
  <h3>上传照片，记录美好</h3>
  <input type="file" id="photo" accept="image/*" />
  <button onclick="uploadPhoto()">上传</button>

  <div class="gallery" id="gallery"></div>
</div>

<script>
const API = "https://YOUR_WORKER_URL"; // 替换为你的 Worker 地址
let token = null;

async function login() {
  const username = document.getElementById('username').value;
  const password = document.getElementById('password').value;

  const res = await fetch(API + '/login', {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify({ username, password })
  });
  const data = await res.json();
  if (data.token) {
    token = data.token;
    document.getElementById('loginCard').style.display = 'none';
    document.getElementById('appCard').style.display = 'block';
    loadPhotos();
  } else {
    alert('登录失败');
  }
}

async function uploadPhoto() {
  const file = document.getElementById('photo').files[0];
  if (!file) return alert('请选择照片');

  const form = new FormData();
  form.append('file', file);

  await fetch(API + '/upload', {
    method: 'POST',
    headers: { 'Authorization': 'Bearer ' + token },
    body: form
  });

  loadPhotos();
}

async function loadPhotos() {
  const res = await fetch(API + '/photos', {
    headers: { 'Authorization': 'Bearer ' + token }
  });
  const photos = await res.json();
  const gallery = document.getElementById('gallery');
  gallery.innerHTML = '';
  photos.forEach(url => {
    const img = document.createElement('img');
    img.src = url;
    gallery.appendChild(img);
  });
}
</script>

</body>
</html>

/* ================= Cloudflare Worker 示例 =================

export default {
  async fetch(req, env) {
    const url = new URL(req.url);

    if (url.pathname === '/login') {
      const { username, password } = await req.json();
      const key = `user:${username}`;
      const saved = await env.USERS.get(key);
      if (!saved) {
        await env.USERS.put(key, password);
      }
      if ((saved && saved === password) || !saved) {
        return Response.json({ token: btoa(username) });
      }
      return Response.json({ error: 'fail' }, { status: 401 });
    }

    if (url.pathname === '/upload') {
      const auth = req.headers.get('Authorization');
      const user = atob(auth.replace('Bearer ', ''));
      const form = await req.formData();
      const file = form.get('file');
      const key = `${user}/${Date.now()}-${file.name}`;
      await env.PHOTOS.put(key, file.stream());
      return Response.json({ ok: true });
    }

    if (url.pathname === '/photos') {
      const auth = req.headers.get('Authorization');
      const user = atob(auth.replace('Bearer ', ''));
      const list = await env.PHOTOS.list({ prefix: user });
      const urls = list.objects.map(o => env.PHOTOS_PUBLIC_URL + '/' + o.key);
      return Response.json(urls);
    }

    return new Response('Not Found', { status: 404 });
  }
}

================= 绑定资源 =================
KV: USERS
R2: PHOTOS
环境变量: PHOTOS_PUBLIC_URL

*/
