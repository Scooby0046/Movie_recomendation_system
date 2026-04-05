# Movie Recommendation Project - Setup Instructions

## Prerequisites
- Python 3.8+
- pip (Python package manager)
- Git

## Installation Steps

### 1. **Clone the Repository**
```bash
cd /Users/praveensharma/Downloads/movie_recommendation-main
```

### 2. **Create Virtual Environment**
```bash
# Create virtual environment
python3 -m venv venv

# Activate virtual environment
source venv/bin/activate  # On macOS/Linux
# or
venv\Scripts\activate  # On Windows
```

### 3. **Install Dependencies**
```bash
pip install -r requirements.txt
```

### 4. **Database Setup**
```bash
# Apply migrations
python manage.py migrate

# Create superuser (admin account)
python manage.py createsuperuser
# Follow the prompts to set username, email, and password
```

### 5. **Run Development Server**
```bash
python manage.py runserver
```
The application will be available at: `http://127.0.0.1:8000/`

### 6. **Access Admin Panel**
Navigate to: `http://127.0.0.1:8000/admin/`
Login with your superuser credentials

---

## Project Structure

```
movie_recommendation-main/
├── manage.py                    # Django management script
├── db.sqlite3                   # SQLite database
├── requirements.txt             # Python dependencies
│
├── movie_recommender/           # Project settings
│   ├── settings.py              # Django configuration
│   ├── urls.py                  # URL routing
│   ├── wsgi.py                  # WSGI configuration
│   └── asgi.py                  # ASGI configuration
│
├── movies/                      # Main Django app
│   ├── models.py                # Database models
│   ├── views.py                 # Business logic
│   ├── urls.py                  # App URL routing
│   ├── admin.py                 # Admin configuration
│   ├── apps.py                  # App configuration
│   ├── migrations/              # Database migrations
│   └── templates/movies/        # HTML templates
│       ├── base.html
│       ├── home.html
│       ├── detail.html
│       ├── recommendations.html
│       ├── watchlist.html
│       └── registration/
│           └── login.html
│
└── frontend/                    # React frontend (optional)
    └── src/
        └── App.js               # React component
```

---

## Key Features

### User Authentication
- Login/Logout system
- User-based movie ratings (liked movies)
- Watchlist per user

### Movie Features
- Search movies via OMDb API
- View movie details (title, year, genre, rating, poster, description)
- Like/favorite movies
- Add movies to watchlist
- Get personalized recommendations

### URLs & Routes

| Route | Description |
|-------|-------------|
| `/` | Home page with movie search |
| `/login/` | User login |
| `/admin/` | Admin panel |
| `/movie/<id>/` | Movie detail page |
| `/like/<id>/` | Like a movie |
| `/watchlist/` | View user's watchlist |
| `/watchlist/<id>/` | Add/remove from watchlist |
| `/recommend/` | Get recommendations |
| `/suggest/` | Search suggestions (AJAX) |

---

## API Configuration

### OMDb API Key
The project uses OMDb API for movie data. The API key is currently in `movies/views.py`:

```python
API_KEY = "6aed4a4e"
```

**To use your own API key:**
1. Go to http://www.omdbapi.com/apikey.aspx
2. Get a free API key
3. Update the `API_KEY` variable in `movies/views.py`

---

## Environment Variables (Optional)

Create a `.env` file in the project root:

```env
SECRET_KEY=your-secret-key-here
DEBUG=True
ALLOWED_HOSTS=localhost,127.0.0.1
OMDB_API_KEY=your-api-key-here
```

Install `python-decouple` to use environment variables:
```bash
pip install python-decouple
```

---

## Troubleshooting

### Issue: "No such table: movies_movie"
**Solution:** Run migrations
```bash
python manage.py makemigrations
python manage.py migrate
```

### Issue: Static files not loading
**Solution:** Collect static files
```bash
python manage.py collectstatic --noinput
```

### Issue: Login redirect not working
**Solution:** Ensure `LOGIN_URL` and `LOGIN_REDIRECT_URL` are set in `settings.py`

### Issue: OMDb API not responding
**Solution:** Check your API key and internet connection. The API is called in `movies/views.py`

---

## Dependencies Explanation

| Package | Version | Purpose |
|---------|---------|---------|
| **Django** | 4.2.27 | Web framework |
| **requests** | 2.31.0 | HTTP library for API calls |
| **python-decouple** | 3.8 | Environment variable management |
| **Pillow** | 10.1.0 | Image processing (for poster handling) |

---

## Development Tips

1. **Run Django shell for testing:**
   ```bash
   python manage.py shell
   ```

2. **Create new migrations after model changes:**
   ```bash
   python manage.py makemigrations
   python manage.py migrate
   ```

3. **Access Django admin for database management:**
   ```
   http://127.0.0.1:8000/admin/
   ```

4. **Debug mode is ON** (change `DEBUG = False` in production)

---

## Next Steps

1. Test the application at `http://127.0.0.1:8000/`
2. Create a superuser account
3. Add movies through the admin panel or search
4. Test the recommendation engine
5. Deploy to production when ready

---

For more info, visit: [Django Documentation](https://docs.djangoproject.com/)
