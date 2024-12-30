<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Movie Website</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            background-color: #121212;
            color: #fff;
        }
        .header {
            background-color: #1e1e1e;
            padding: 20px;
            text-align: center;
        }
        .header .logo {
            display: inline-block;
            font-size: 24px;
            font-weight: bold;
            color: #f39c12;
        }
        .header .logo span {
            color: #fff;
        }
        .movie-container {
            display: flex;
            flex-wrap: wrap;
            justify-content: center;
            gap: 20px;
            padding: 20px;
        }
        .movie {
            background-color: #1e1e1e;
            border: 1px solid #333;
            border-radius: 8px;
            overflow: hidden;
            width: 300px;
        }
        .movie img {
            width: 100%;
            height: auto;
        }
        .movie .details {
            padding: 15px;
        }
        .movie .details h2 {
            margin: 0 0 10px;
            font-size: 18px;
            color: #f39c12;
        }
        .movie .details p {
            margin: 0 0 10px;
        }
        .popup {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.8);
            display: flex;
            justify-content: center;
            align-items: center;
            z-index: 1000;
        }
        .popup-content {
            background-color: #1e1e1e;
            padding: 20px;
            text-align: center;
            border-radius: 8px;
        }
        .popup-content button {
            background-color: #f39c12;
            border: none;
            padding: 10px 20px;
            color: #fff;
            font-size: 16px;
            cursor: pointer;
            margin: 10px;
            border-radius: 5px;
        }
        .popup-content button:hover {
            background-color: #e67e22;
        }
        .pagination {
            display: flex;
            justify-content: center;
            padding: 20px;
            gap: 5px;
        }
        .pagination button {
            background-color: #f39c12
            border: none;
            padding: 10px 15px;
            color: #000;
            font-size: 14px;
            cursor: pointer;
            border-radius: 5px;
        }
        .pagination button.active {
            background-color: #f39c12
            color: #fff;
        }
        .pagination button:hover {
            background-color: #f39c12
        }
        .sidebar {
    background-color: #1e1e1e;
    color: #fff;
    padding: 20px;
    width: 250px;
    min-height: 100vh;
    position: fixed;
    top: 0;
    left: 0;
    overflow-y: auto;
    border-right: 1px solid #333;
}

.sidebar h2 {
    font-size: 20px;
    margin-bottom: 15px;
    color: #f39c12;
}

.sidebar ul {
    list-style: none;
    padding: 0;
    margin: 0;
}

.sidebar ul li {
    margin-bottom: 10px;
}

.sidebar ul li a {
    text-decoration: none;
    color: #fff;
    transition: color 0.3s;
}

.sidebar ul li a:hover {
    color: #f39c12;
}
.hamburger {
    display: none;
    font-size: 24px;
    cursor: pointer;
    color: #f39c12;
    position: absolute;
    top: 20px;
    right: 20px;
}

/* استایل منو */
.nav-menu {
    list-style: none;
    margin: 0;
    padding: 0;
    display: flex;
    gap: 15px;
}

.nav-menu li {
    display: inline;
}

.nav-menu a {
    text-decoration: none;
    color: #fff;
    font-size: 16px;
}

/* مخفی کردن منو در موبایل */
@media (max-width: 768px) {
    .hamburger {
        display: block;
    }

    .nav-menu {
        display: none;
        flex-direction: column;
        position: absolute;
        top: 60px;
        right: 20px;
        background-color: #1e1e1e;
        border: 1px solid #333;
        border-radius: 8px;
        padding: 10px;
        width: 200px;
        z-index: 1000;
    }

    .nav-menu.active {
        display: flex;
    }

    .nav-menu li {
        margin-bottom: 10px;
    }

    .nav-menu li:last-child {
        margin-bottom: 0;
    }
}

    </style>
    <link rel="icon" href="icon/DAL1.png" type="image.jpg">
</head>
<body>
    <div class="popup" id="agePopup">
        <div class="popup-content">
            <p>آیا شما 18 سال سن دارید؟
                <br>⚠️هشدار این متحوای بزرگسالان است
            </p>
            <button onclick="acceptAge()">Yes</button>
            <button onclick="denyAge()">No</button>
        </div>
    </div>
        <div class="hamburger" onclick="toggleMenu()">☰</div>
        <ul class="nav-menu" id="navMenu">
            <li><a href="#">Home</a></li>
            <li><a href="#">Categories</a></li>
            <li><a href="#">Actors</a></li>
            <li><a href="#">Contact</a></li>
        </ul>
    </div>
    
    
    

    <div class="header">
        <div class="logo">Sex<span>ino</span></div>
    </div>
    <div class="movie-container" id="movieContainer"></div>

    <div class="pagination" id="pagination"></div>

    <img src="" alt="">
    <img src="" alt="">
    <script>
       const movies = [
    { title: "مادر حامله نمیشود و از کیر پسر تغذیه میکند", genre: "Action", duration: 120, img: "images/6856360-320x180 (1).jpg" },
    { title: "خواهر ناتنی با برادر ناتنی سکس میکنن.", genre: "Drama", duration: 100, img: "images/8681266-320x180.jpg" },
    { title: "Movie 3", genre: "Action", duration: 110, img: "./" },
    { title: "Movie 4", genre: "Comedy", duration: 90, img: "images/8681266-320x180.jpg" },
    { title: "Movie 4", genre: "Comedy", duration: 90, img: "images/6856360-320x180 (1).jpg" },
    { title: "Movie 4", genre: "Comedy", duration: 90, img: "images/img3.jpg" },
    { title: "Movie 4", genre: "Comedy", duration: 90, img: "path/to/image4.jpg" },
    { title: "Movie 4", genre: "Comedy", duration: 90, img: "path/to/image4.jpg" },
    { title: "Movie 4", genre: "Comedy", duration: 90, img: "path/to/image4.jpg" },
    { title: "Movie 4", genre: "Comedy", duration: 90, img: "path/to/image4.jpg" },
    { title: "Movie 4", genre: "Comedy", duration: 90, img: "path/to/image4.jpg" },
    { title: "Movie 4", genre: "Comedy", duration: 90, img: "path/to/image4.jpg" },
    { title: "Movie 4", genre: "Comedy", duration: 90, img: "path/to/image4.jpg" },
    { title: "Movie 4", genre: "Comedy", duration: 90, img: "path/to/image4.jpg" },
    { title: "Movie 4", genre: "Comedy", duration: 90, img: "path/to/image4.jpg" },
    { title: "Movie 4", genre: "Comedy", duration: 90, img: "path/to/image4.jpg" },
    { title: "Movie 4", genre: "Comedy", duration: 90, img: "path/to/image4.jpg" },

    // مسیر تصاویر برای بقیه فیلم‌ها
]

        const moviesPerPage = 9;
        let currentPage = 1;

        function renderMovies(page) {
            const container = document.getElementById('movieContainer');
            container.innerHTML = '';
            const start = (page - 1) * moviesPerPage;
            const end = start + moviesPerPage;
            const moviesToShow = movies.slice(start, end);

            moviesToShow.forEach(movie => {
                const movieElement = document.createElement('div');
                movieElement.classList.add('movie');
                movieElement.innerHTML = `
                    <img src="${movie.img}" alt="Movie Poster">
                    <div class="details">
                        <h2>${movie.title}</h2>
                        <p>Genre: ${movie.genre}</p>
                        <p>Duration: ${movie.duration} mins</p>
                    </div>
                `;
                container.appendChild(movieElement);
            });
        }

        function renderPagination() {
            const pagination = document.getElementById('pagination');
            pagination.innerHTML = '';
            const totalPages = Math.ceil(movies.length / moviesPerPage);

            for (let i = 1; i <= totalPages; i++) {
                const button = document.createElement('button');
                button.textContent = i;
                if (i === currentPage) {
                    button.classList.add('active');
                }
                button.addEventListener('click', () => {
                    currentPage = i;
                    renderMovies(currentPage);
                    renderPagination();
                });
                pagination.appendChild(button);
            }
        }

        function acceptAge() {
            document.getElementById('agePopup').style.display = 'none';
            renderMovies(currentPage);
            renderPagination();
        }

        function denyAge() {
            alert('You must be over 18 to access this site.');
            window.location.href = 'https://www.google.com';
        }

        document.addEventListener('DOMContentLoaded', () => {
            renderMovies(currentPage);
            renderPagination();
        });
        function toggleMenu() {
    const menu = document.getElementById('navMenu');
    menu.classList.toggle('active');
}
function renderMovies(page) {
    const container = document.getElementById('movieContainer');
    container.innerHTML = '';
    const start = (page - 1) * moviesPerPage;
    const end = start + moviesPerPage;
    const moviesToShow = movies.slice(start, end);

    moviesToShow.forEach(movie => {
        const movieElement = document.createElement('div');
        movieElement.classList.add('movie');
        movieElement.innerHTML = `
            <a href="https://example.com/${movie.title.replace(/\s+/g, '-').toLowerCase()}" target="_blank" style="text-decoration: none; color: inherit;">
                <img src="${movie.img}" alt="Movie Poster">
                <div class="details">
                    <h2>${movie.title}</h2>
                    <p>Genre: ${movie.genre}</p>
                    <p>Duration: ${movie.duration} mins</p>
                </div>
            </a>
        `;
        container.appendChild(movieElement);
    });
}

    </script>
</body>
</html>
