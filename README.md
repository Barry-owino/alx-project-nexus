# Backend Development Journey 🚀

This repository documents my backend development journey with **Django, Django REST Framework (DRF), CI/CD, and DevOps tools**.  
It combines multiple projects, concepts, and hands-on implementations into one reference guide.

---

## 📌 Table of Contents
1. [Introduction](#introduction)
2. [Projects Overview](#projects-overview)
   - [Airbnb Clone (Security & Tracking)](#airbnb-clone-security--tracking)
   - [Messaging App (CI/CD & Caching)](#messaging-app-cicd--caching)
   - [Travel App (Listings, Bookings, Reviews)](#travel-app-listings-bookings-reviews)
   - [Facebook Clone (Social Media API)](#facebook-clone-social-media-api)
   - [Portfolio App (Blog & Showcase)](#portfolio-app-blog--showcase)
3. [Core Backend Concepts](#core-backend-concepts)
   - Models, Views, CRUD
   - Authentication & Custom Users
   - Middleware & Signals
   - Caching & Security
4. [API Testing & Documentation](#api-testing--documentation)
   - Postman
   - Swagger
   - curl
5. [CI/CD & Deployment](#cicd--deployment)
   - GitHub Actions
   - Jenkins
   - Docker
   - Kubernetes
6. [Best Practices & Learnings](#best-practices--learnings)

---

## 🏁 Introduction
This document brings together everything I have been building and learning as a backend developer.  
It covers real-world projects, practical implementations, and DevOps practices to deliver secure, scalable, and maintainable applications.

---

## 🛠 Projects Overview

### 🏨 Airbnb Clone (Security & Tracking)
A Django-based project focusing on **security and visitor tracking**.

**Highlights:**
- Implemented **custom middleware** to log visitor IP addresses, pages visited, and timestamps.  
- Stored logs in `requests.log` for analysis.  
- Added **cron jobs** to automate log rotation and monitoring.  
- Security-focused with suspicious activity tracking.

```python
class RequestLoggingMiddleware:
    def __init__(self, get_response):
        self.get_response = get_response

    def __call__(self, request):
        ip = request.META.get("REMOTE_ADDR")
        path = request.path
        with open("requests.log", "a") as f:
            f.write(f"{ip} visited {path}\n")
        return self.get_response(request)
💬 Messaging App (CI/CD & Caching)
A Django messaging app built with modern CI/CD pipelines.

Highlights:

Caching using LocMemCache to optimize message retrieval.

CI/CD setup with:

GitHub Actions → tests, linting, coverage, Docker build.

Jenkins → pipeline for automated testing and Docker image publishing.

Containerized using Docker and deployed to Kubernetes for scalability.

python
Copy code
# Example of caching a view
from django.views.decorators.cache import cache_page

@cache_page(60 * 15)  # cache for 15 minutes
def message_list(request):
    ...
✈️ Travel App (Listings, Bookings, Reviews)
A Django REST Framework project simulating a travel booking platform.

Highlights:

Models:

Listing → travel packages

Booking → reservations

Review → user feedback

Seeder commands to populate test data.

API endpoints built with DRF serializers and viewsets.

python
Copy code
class Listing(models.Model):
    title = models.CharField(max_length=255)
    price = models.DecimalField(max_digits=10, decimal_places=2)
    description = models.TextField()
📱 Facebook Clone (Social Media API)
A social media backend built with Django & DRF.

Highlights:

Authentication (login, logout, registration).

Core features:

Posts

Comments

Likes

Follows

Notifications

JWT/Token authentication for secure API access.

Deployment-ready with Docker.

🌐 Portfolio App (Blog & Showcase)
A Django project to showcase my work and write blog posts.

Highlights:

One app: portfolio_app

Features:

Personal portfolio showcase

Blog section with posts and categories

Custom styling with a yellow, vintage-tech theme

Integrated DRF APIs for blog content.

⚙️ Core Backend Concepts
📌 Models, Views, CRUD
Models define the database schema.

Views handle requests and responses.

CRUD implemented with Django ORM and DRF serializers.

🔐 Authentication & Custom Users
Extended AbstractUser with date_of_birth and profile_photo.

Configured AUTH_USER_MODEL in settings.py.

Integrated into admin and APIs.

🧩 Middleware & Signals
Middleware → request logging, security checks.

Signals → perform actions like sending notifications when a model is saved.

python
Copy code
from django.db.models.signals import post_save
from django.dispatch import receiver

@receiver(post_save, sender=User)
def create_profile(sender, instance, created, **kwargs):
    if created:
        Profile.objects.create(user=instance)
⚡ Caching & Security
LocMemCache for performance.

Security measures:

Input validation

IP tracking

Authentication & authorization checks

📡 API Testing & Documentation
🧪 Postman
Tested endpoints for CRUD, auth, and data retrieval.

Collections saved for reuse.

📖 Swagger
Auto-generated documentation with drf-yasg.

Interactive API docs for developers.

python
Copy code
# settings.py
INSTALLED_APPS = [
    ...,
    'drf_yasg',
]
🖥 curl
Quick command-line API testing.

bash
Copy code
# Example: Fetch all listings
curl -X GET http://127.0.0.1:8000/api/listings/
🔄 CI/CD & Deployment
🔧 GitHub Actions
Workflow to run tests, lint code, and build Docker images.

🏗 Jenkins
Automated pipeline for testing and deployment.

Integrated with DockerHub for image publishing.

🐳 Docker
Containerized all projects for portability.

Commands used:

bash
Copy code
docker build -t myapp .
docker run -p 8000:8000 myapp
☸️ Kubernetes
Managed container orchestration.

Deployed Django apps in pods with load balancing.

✅ Best Practices & Learnings
Always use virtual environments for Django projects.

Separate settings for development and production.

Automate with CI/CD pipelines.

Use Postman/Swagger/curl for reliable API testing.

Embrace Docker & Kubernetes for scalable deployments.

Implement middleware, signals, and caching for performance and maintainability.

🎯 Conclusion
This README brings together my backend journey using Django, DRF, and DevOps tools.
It documents real projects like the Airbnb clone, Messaging app, Travel app, Facebook clone, and Portfolio app — all connected by best practices in backend engineering.
