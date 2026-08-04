
const CACHE_NAME = 'easy-camera-v1';
const urlsToCache = [
  './',
  './index.html',
  './manifest.json'
];

// アプリのインストール時にファイルをキャッシュ（保存）する
self.addEventListener('install', (event) => {
  event.waitUntil(
    caches.open(CACHE_NAME).then((cache) => {
      return cache.addAll(urlsToCache);
    })
  );
});

// ネット接続がない場合でもキャッシュから読み込む
self.addEventListener('fetch', (event) => {
  event.respondWith(
    caches.match(event.request).then((response) => {
      return response || fetch(event.request);
    })
  );
});
