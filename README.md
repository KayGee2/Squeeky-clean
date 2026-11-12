# Ukuhlanza (Ltd): Cleaning Company Website

A responsive website for a fictional South African cleaning company. It has a single-page marketing site, plus a welcome page with sign-in, registration and an instant quote calculator. Built with Bootstrap 5, custom CSS and vanilla JavaScript.

Features

Landing page (home.html)

Sticky card-style navbar with smooth-scroll links to each section
Hero, services, reviews, pricing and contact-form sections
Cards that float in as you scroll, using the IntersectionObserver API
Hover effects on service, review and pricing cards
Navbar shows "Hi, Name / Sign out" when signed in, or "Sign in" when not

Welcome page (index.html)

Tabbed interface (Bootstrap pills): Sign in, Register, Quick quote
Form validation with Bootstrap's validation styles and the browser's Constraint Validation API
Password hashing (SHA-256 via the Web Crypto API) before saving
Show/hide password toggle
Quote calculator that returns an estimated price range from service type, size and frequency
"Continue as guest" option

General

Mobile-first, responsive layout
Brand colours defined once as CSS custom properties
Accessibility: semantic HTML, ARIA roles and labels, visible focus outlines, and prefers-reduced-motion support
Content stays visible if JavaScript is disabled
Tech stack
Area	Tools
Markup	HTML5
Styling	CSS3 (custom properties, animations), Bootstrap 5
Scripting	Vanilla JavaScript (ES5-style, no build step)
Fonts and icons	Google Fonts (Dosis, Roboto), Font Awesome 6
Storage	localStorage
Project structure
ukuhlanza/
├── index.html              # Welcome page: sign in, register, quick quote
├── home.html               # Main landing page
├── style.css               # Landing page styles
├── auth.css                # Welcome page styles
├── auth.js                 # Auth and quote logic
├── session.js              # Navbar sign-in state and form pre-fill
├── css/bootstrap.min.css
├── js/bootstrap.bundle.js
└── (images)                # Logo, service, review and background photos
Getting started
Download or clone the project.
Put bootstrap.min.css in css/ and bootstrap.bundle.js in js/.
Place the images in the project root. The code expects names such as ukuhlanza_A_skyline_teal.png, counter.jpg, hom.jpg, office.jpg, cleaning.jpg and sign_in_background_1_.jpeg.
Serve the folder with any local server, because image paths start with /:
bash
   python -m http.server 8000
Open http://localhost:8000/index.html.
How it works
Authentication demo (auth.js)
Users are stored as an array of { name, email, hash } objects under the key ukuhlanza_users.
On register, the app validates the form, checks the email isn't already used, hashes the password, saves the user and starts a session.
On sign in, it finds the user by email, hashes the typed password and compares it to the stored hash.
The active session is saved under ukuhlanza_session. After sign-in, the user is redirected to home.html.
Quote calculator
estimate = basePrice[service][size] × (1 − frequencyDiscount)
range    = estimate × 0.9  to  estimate × 1.1   (rounded to the nearest R10)
Service	Small	Medium	Large
Home	R450	R650	R950
Office	R600	R1 100	R1 800
Deep clean	R900	R1 400	R2 200

Frequency discounts: once-off 0%, monthly 5%, every 2 weeks 10%, weekly 15%. The prices are placeholders and can be changed in the PRICES and DISCOUNT objects.

Scroll animations

Elements with the .reveal class are watched by an IntersectionObserver. When one enters the viewport it gets the .visible class, and CSS plays the floatIn animation. Each card gets a staggered delay, and the observer stops watching it afterwards.

Security notes

This project is a demonstration of front-end logic only.

localStorage is readable by anyone using the same browser. It is not suitable for real accounts.
SHA-256 is a fast general-purpose hash. A production system should hash on the server with a slow, salted algorithm such as bcrypt or Argon2.
The "Continue with Google" button signs in a placeholder user. A real version would use Google Identity Services and verify the ID token on a server.
The contact form has action="#", so it does not send data anywhere yet.
Roadmap
 Backend for authentication and bookings (Node.js or similar)
 Real Google sign-in
 Send contact and quote requests by email
 Replace placeholder text and reviews with real content
 Booking calendar
What I learned
Structuring CSS with design tokens and a consistent section system
Using browser APIs (IntersectionObserver, Web Crypto, localStorage) without libraries
Building accessible forms and motion-safe animations
The limits of client-side security, and what a production system needs
Author

Kagisho Madigwe: GitHub
