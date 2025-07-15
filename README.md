<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Mini Netflix</title>
  <style>
    body {
      margin: 0;
      font-family: 'Segoe UI', sans-serif;
      background-color: #121212;
      color: #fff;
    }
    header {
      text-align: center;
      padding: 20px;
    }
    .movie-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
      gap: 16px;
      padding: 20px;
    }
    .movie-card {
      background-color: #1e1e1e;
      border-radius: 8px;
      overflow: hidden;
      transition: transform 0.2s;
    }
    .movie-card:hover {
      transform: scale(1.05);
    }
    .movie-card img {
      width: 100%;
      display: block;
    }
  </style>
</head>
<body>
  <header>
    <h1>🎬 Mini Netflix</h1>
  </header>
  <main>
    <section id="movies" class="movie-grid"></section>
  </main>
  <script>
    const API_KEY = '3633b89cd5c59bab33c1e3a7f0615f42';
    const API_URL = `https://api.themoviedb.org/3/trending/movie/week?api_key=${API_KEY}`;
    const IMG_BASE = 'https://image.tmdb.org/t/p/w500';

    async function fetchMovies() {
      const res = await fetch(API_URL);
      const data = await res.json();
      displayMovies(data.results);
    }

    function displayMovies(movies) {
      const container = document.getElementById('movies');
      container.innerHTML = movies.map(movie => `
        <div class="movie-card">
          <img src="${IMG_BASE}${movie.poster_path}" alt="${movie.title}" />
        </div>
      `).join('');
    }

    fetchMovies();
  </script>
</body>
</html>
