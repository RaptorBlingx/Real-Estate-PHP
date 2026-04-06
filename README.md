<h1 align="center">
  <br>
  <img src="images/icon-1.png" alt="MyHome Logo" width="80">
  <br>
  MyHome — Real Estate Platform
  <br>
</h1>

<p align="center">
  A full-stack real estate web application built with <strong>PHP</strong>, <strong>MySQL</strong>, and <strong>vanilla JavaScript</strong> that lets users list, search, save, and enquire about properties — with a complete admin panel for platform management.
</p>

<p align="center">
  <a href="https://youtu.be/l38o5Jn62S8">
    <img src="https://img.shields.io/badge/▶%20Watch%20on-YouTube-red?style=for-the-badge&logo=youtube" alt="YouTube Walkthrough">
  </a>
  &nbsp;
  <img src="https://img.shields.io/badge/PHP-8%2B-777BB4?style=for-the-badge&logo=php&logoColor=white" alt="PHP">
  &nbsp;
  <img src="https://img.shields.io/badge/MySQL-8%2B-4479A1?style=for-the-badge&logo=mysql&logoColor=white" alt="MySQL">
  &nbsp;
  <img src="https://img.shields.io/badge/CSS3-Responsive-1572B6?style=for-the-badge&logo=css3&logoColor=white" alt="CSS3">
</p>

---

## 📺 Video Walkthrough

> Watch the full project walkthrough on YouTube:  
> **[https://youtu.be/l38o5Jn62S8](https://youtu.be/l38o5Jn62S8)**

[![YouTube Walkthrough](https://img.youtube.com/vi/l38o5Jn62S8/maxresdefault.jpg)](https://youtu.be/l38o5Jn62S8)

---

## 📋 Table of Contents

- [Overview](#-overview)
- [Features](#-features)
- [Tech Stack](#-tech-stack)
- [Project Structure](#-project-structure)
- [Database Schema](#-database-schema)
- [Getting Started](#-getting-started)
- [Screenshots](#-screenshots)
- [Contributing](#-contributing)
- [License](#-license)

---

## 🏠 Overview

**MyHome** is a feature-rich real estate listing platform where:

- **Buyers / Renters** can browse listings, filter by location, type, price range, and offer type, save favourites, and send direct enquiries to sellers.
- **Sellers / Landlords** can register an account, post detailed property listings with up to 5 images, and track incoming enquiry requests.
- **Admins** have a dedicated panel to manage all listings, users, admins, and messages.

---

## ✨ Features

### 👤 User-Facing
| Feature | Description |
|---|---|
| 🔍 Smart Search | Filter by city, property type (Flat / House / Shop), offer type (Sale / Resale / Rent), and budget range |
| 🏡 Property Listings | View the latest listings with images, BHK, price, location, and key amenities at a glance |
| 📝 Post Property | Publish a detailed listing with up to 5 photos, 30+ attributes (floors, age, carpet area, amenities) |
| ❤️ Save Properties | Bookmark favourite properties to a personal saved list |
| 📨 Send Enquiry | Contact the property owner directly from any listing |
| 📬 Requests Dashboard | Track all sent and received enquiry requests |
| 🔐 Auth | Register / Login / Logout with cookie-based sessions |
| 👤 Profile Management | Update personal account details |

### 🛡️ Admin Panel (`/admin`)
| Feature | Description |
|---|---|
| 📊 Dashboard | At-a-glance counts: listings, users, admins, messages |
| 🏘️ Manage Listings | View and delete any property on the platform |
| 👥 Manage Users | View and remove user accounts |
| 🧑‍💼 Manage Admins | View and remove admin accounts |
| 💬 Messages | Read contact-form messages sent via the Contact page |
| 🔐 Admin Auth | Separate admin register / login / logout flow |

---

## 🛠️ Tech Stack

| Layer | Technology |
|---|---|
| **Backend** | PHP 8+ (PDO for database access) |
| **Database** | MySQL 8+ |
| **Frontend** | HTML5, CSS3 (custom responsive stylesheet), Vanilla JavaScript |
| **Icons** | Font Awesome 6.2 (CDN) |
| **Alerts** | SweetAlert 2.1 (CDN) |
| **Architecture** | Multi-page application (MPA) with reusable PHP components |

---

## 📁 Project Structure

```
Real-Estate-PHP/
│
├── admin/                    # Admin panel pages
│   ├── dashboard.php         # Admin overview (listings, users, admins, messages counts)
│   ├── listings.php          # View & manage all property listings
│   ├── users.php             # View & manage registered users
│   ├── admins.php            # View & manage admin accounts
│   ├── messages.php          # View contact-form messages
│   ├── view_property.php     # Admin property detail view
│   ├── login.php             # Admin login
│   ├── register.php          # Admin registration
│   └── update.php            # Admin profile update
│
├── components/               # Shared PHP includes
│   ├── connect.php           # PDO database connection + helper functions
│   ├── user_header.php       # User-facing navigation bar
│   ├── admin_header.php      # Admin navigation bar
│   ├── footer.php            # Site-wide footer
│   ├── message.php           # SweetAlert flash messages
│   ├── save_send.php         # Save / send-enquiry form handlers
│   ├── user_logout.php       # User logout handler
│   └── admin_logout.php      # Admin logout handler
│
├── css/
│   ├── style.css             # User-facing styles (responsive)
│   └── admin_style.css       # Admin panel styles
│
├── js/
│   ├── script.js             # User-facing JavaScript
│   └── admin_script.js       # Admin JavaScript
│
├── images/                   # Static assets (icons, backgrounds, illustrations)
├── uploaded_files/           # User-uploaded property images (runtime)
│
├── home.php                  # Landing page with hero search form & latest listings
├── listings.php              # Full property listing page
├── search.php                # Search results page
├── view_property.php         # Single property detail page
├── post_property.php         # Create new property listing (auth required)
├── update_property.php       # Edit existing listing (auth required)
├── my_listings.php           # User's own listings (auth required)
├── saved.php                 # User's saved / favourited properties (auth required)
├── requests.php              # User's enquiry requests inbox/outbox (auth required)
├── dashboard.php             # User dashboard (auth required)
├── update.php                # User profile update (auth required)
├── login.php                 # User login
├── register.php              # User registration
├── about.php                 # About page
└── contact.php               # Contact & FAQ page
```

---

## 🗄️ Database Schema

The application uses a MySQL database named **`home_db`**. Create the following tables:

```sql
-- Users
CREATE TABLE `users` (
  `id`       VARCHAR(20)  PRIMARY KEY,
  `name`     VARCHAR(100) NOT NULL,
  `email`    VARCHAR(100) NOT NULL UNIQUE,
  `password` VARCHAR(255) NOT NULL,
  `image`    VARCHAR(100) DEFAULT ''
);

-- Admins
CREATE TABLE `admins` (
  `id`       VARCHAR(20)  PRIMARY KEY,
  `name`     VARCHAR(100) NOT NULL,
  `email`    VARCHAR(100) NOT NULL UNIQUE,
  `password` VARCHAR(255) NOT NULL,
  `image`    VARCHAR(100) DEFAULT ''
);

-- Properties
CREATE TABLE `property` (
  `id`             VARCHAR(20)  PRIMARY KEY,
  `user_id`        VARCHAR(20)  NOT NULL,
  `property_name`  VARCHAR(50)  NOT NULL,
  `address`        VARCHAR(100) NOT NULL,
  `price`          BIGINT       NOT NULL,
  `type`           VARCHAR(20)  NOT NULL,   -- flat | house | shop
  `offer`          VARCHAR(20)  NOT NULL,   -- sale | resale | rent
  `status`         VARCHAR(30)  NOT NULL,   -- ready to move | under construction
  `furnished`      VARCHAR(20)  NOT NULL,   -- furnished | semi-furnished | unfurnished
  `bhk`            INT          NOT NULL,
  `deposite`       BIGINT       NOT NULL,
  `bedroom`        INT          NOT NULL,
  `bathroom`       INT          NOT NULL,
  `balcony`        INT          NOT NULL,
  `carpet`         BIGINT       NOT NULL,
  `age`            INT          NOT NULL,
  `total_floors`   INT          NOT NULL,
  `room_floor`     INT          NOT NULL,
  `loan`           VARCHAR(20)  NOT NULL,   -- available | not available
  `lift`           VARCHAR(5)   DEFAULT 'no',
  `security_guard` VARCHAR(5)   DEFAULT 'no',
  `play_ground`    VARCHAR(5)   DEFAULT 'no',
  `garden`         VARCHAR(5)   DEFAULT 'no',
  `water_supply`   VARCHAR(5)   DEFAULT 'no',
  `power_backup`   VARCHAR(5)   DEFAULT 'no',
  `parking_area`   VARCHAR(5)   DEFAULT 'no',
  `gym`            VARCHAR(5)   DEFAULT 'no',
  `shopping_mall`  VARCHAR(5)   DEFAULT 'no',
  `hospital`       VARCHAR(5)   DEFAULT 'no',
  `school`         VARCHAR(5)   DEFAULT 'no',
  `market_area`    VARCHAR(5)   DEFAULT 'no',
  `image_01`       VARCHAR(100) NOT NULL,
  `image_02`       VARCHAR(100) DEFAULT '',
  `image_03`       VARCHAR(100) DEFAULT '',
  `image_04`       VARCHAR(100) DEFAULT '',
  `image_05`       VARCHAR(100) DEFAULT '',
  `description`    TEXT,
  `date`           TIMESTAMP    DEFAULT CURRENT_TIMESTAMP
);

-- Saved / Favourites
CREATE TABLE `saved` (
  `id`          INT          AUTO_INCREMENT PRIMARY KEY,
  `user_id`     VARCHAR(20)  NOT NULL,
  `property_id` VARCHAR(20)  NOT NULL
);

-- Enquiry Requests
CREATE TABLE `requests` (
  `id`          INT          AUTO_INCREMENT PRIMARY KEY,
  `sender`      VARCHAR(20)  NOT NULL,
  `receiver`    VARCHAR(20)  NOT NULL,
  `property_id` VARCHAR(20)  NOT NULL,
  `date`        TIMESTAMP    DEFAULT CURRENT_TIMESTAMP
);

-- Contact Messages
CREATE TABLE `messages` (
  `id`      INT          AUTO_INCREMENT PRIMARY KEY,
  `name`    VARCHAR(100) NOT NULL,
  `email`   VARCHAR(100) NOT NULL,
  `number`  VARCHAR(20)  NOT NULL,
  `message` TEXT         NOT NULL,
  `date`    TIMESTAMP    DEFAULT CURRENT_TIMESTAMP
);
```

---

## 🚀 Getting Started

### Prerequisites

- **PHP** 8.0 or higher
- **MySQL** 8.0 or higher
- A local server environment: [XAMPP](https://www.apachefriends.org/) / [WAMP](https://www.wampserver.com/) / [Laragon](https://laragon.org/) / [MAMP](https://www.mamp.info/)

### Installation

1. **Clone the repository**

   ```bash
   git clone https://github.com/RaptorBlingx/Real-Estate-PHP.git
   ```

2. **Move files to your web server root**

   ```bash
   # For XAMPP on Windows
   cp -r Real-Estate-PHP/ C:/xampp/htdocs/Real-Estate-PHP

   # For XAMPP on Linux/macOS
   cp -r Real-Estate-PHP/ /opt/lampp/htdocs/Real-Estate-PHP
   ```

3. **Create the database**

   Open [phpMyAdmin](http://localhost/phpmyadmin) and create a new database named **`home_db`**, then run the SQL statements from the [Database Schema](#-database-schema) section above.

4. **Configure the database connection**

   Open `components/connect.php` and update the credentials if needed:

   ```php
   $db_name      = 'mysql:host=localhost;dbname=home_db';
   $db_user_name = 'root';
   $db_user_pass = '';          // ← add your MySQL password here
   ```

5. **Ensure the upload directory is writable**

   ```bash
   chmod 755 uploaded_files/
   ```

6. **Launch the application**

   Open your browser and navigate to:

   ```
   http://localhost/Real-Estate-PHP/home.php
   ```

   Admin panel:

   ```
   http://localhost/Real-Estate-PHP/admin/login.php
   ```

---

## 🖼️ Screenshots

| Page | Description |
|---|---|
| **Home** | Hero search bar + latest 6 listings + services section |
| **Listings** | Full paginated property grid with save & enquiry buttons |
| **Post Property** | Detailed form: 30+ fields, amenity checkboxes, 5 image uploads |
| **User Dashboard** | Counts for listings, requests sent/received, saved properties |
| **Admin Dashboard** | Platform-wide stats: total listings, users, admins, messages |

---

## 🤝 Contributing

Contributions, issues, and feature requests are welcome!

1. Fork the project
2. Create your feature branch: `git checkout -b feature/amazing-feature`
3. Commit your changes: `git commit -m 'Add amazing feature'`
4. Push to the branch: `git push origin feature/amazing-feature`
5. Open a Pull Request

---

## 📄 License

This project is open source and available under the [MIT License](LICENSE).

---

<p align="center">
  Made with ❤️ — happy coding!
</p>
