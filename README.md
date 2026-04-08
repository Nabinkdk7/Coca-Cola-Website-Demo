
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Coca-Cola - Open Happiness</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        :root {
            --primary-red: #FF0000;
            --dark-red: #CC0000;
            --bg-dark: #0f0f0f;
            --bg-light: #f8f8f8;
            --text-dark: #1a1a1a;
            --text-light: #ffffff;
            --accent-gold: #d4af37;
            --shadow-sm: 0 4px 6px rgba(0, 0, 0, 0.07);
            --shadow-md: 0 10px 15px rgba(0, 0, 0, 0.1);
            --shadow-lg: 0 20px 40px rgba(0, 0, 0, 0.15);
        }

        html {
            scroll-behavior: smooth;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            color: var(--text-dark);
            background-color: var(--bg-light);
            overflow-x: hidden;
        }

        /* ==================== LOADING ANIMATION ==================== */
        .loader {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: var(--bg-dark);
            display: flex;
            align-items: center;
            justify-content: center;
            z-index: 9999;
            animation: fadeOut 0.6s ease-in-out 2s forwards;
        }

        .loader-content {
            text-align: center;
        }

        .loader-circle {
            width: 60px;
            height: 60px;
            border: 4px solid rgba(255, 0, 0, 0.2);
            border-top-color: var(--primary-red);
            border-radius: 50%;
            animation: spin 1s linear infinite;
            margin: 0 auto 20px;
        }

        .loader-text {
            color: var(--text-light);
            font-size: 16px;
            font-weight: 600;
            letter-spacing: 2px;
            animation: pulse 1.5s ease-in-out infinite;
        }

        @keyframes spin {
            to { transform: rotate(360deg); }
        }

        @keyframes pulse {
            0%, 100% { opacity: 0.6; }
            50% { opacity: 1; }
        }

        @keyframes fadeOut {
            from { opacity: 1; visibility: visible; }
            to { opacity: 0; visibility: hidden; }
        }

        /* ==================== NAVIGATION ==================== */
        nav {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            background: rgba(255, 255, 255, 0.95);
            backdrop-filter: blur(10px);
            z-index: 1000;
            padding: 1rem 2rem;
            box-shadow: var(--shadow-md);
            transition: all 0.3s ease;
        }

        nav.scrolled {
            padding: 0.5rem 2rem;
            box-shadow: 0 10px 30px rgba(255, 0, 0, 0.1);
        }

        nav.dark-bg {
            background: rgba(0, 0, 0, 0.95);
            color: var(--text-light);
        }

        .nav-container {
            max-width: 1400px;
            margin: 0 auto;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .logo {
            font-size: 28px;
            font-weight: 900;
            color: var(--primary-red);
            letter-spacing: -1px;
            text-transform: uppercase;
            background: linear-gradient(135deg, var(--primary-red), var(--dark-red));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            transition: all 0.3s ease;
        }

        .logo:hover {
            transform: scale(1.05);
        }

        .nav-menu {
            display: flex;
            gap: 2rem;
            list-style: none;
            align-items: center;
        }

        .nav-menu a {
            text-decoration: none;
            color: var(--text-dark);
            font-weight: 600;
            font-size: 14px;
            position: relative;
            transition: color 0.3s ease;
            text-transform: uppercase;
            letter-spacing: 0.5px;
        }

        nav.dark-bg .nav-menu a {
            color: var(--text-light);
        }

        .nav-menu a::after {
            content: '';
            position: absolute;
            bottom: -5px;
            left: 0;
            width: 0;
            height: 2px;
            background: var(--primary-red);
            transition: width 0.3s ease;
        }

        .nav-menu a:hover::after,
        .nav-menu a.active::after {
            width: 100%;
        }

        .nav-cta {
            background: var(--primary-red);
            color: var(--text-light);
            padding: 0.7rem 1.5rem;
            border-radius: 50px;
            font-weight: 700;
            border: none;
            cursor: pointer;
            transition: all 0.3s ease;
            text-transform: uppercase;
            font-size: 12px;
            letter-spacing: 1px;
        }

        .nav-cta:hover {
            background: var(--dark-red);
            transform: translateY(-2px);
            box-shadow: 0 10px 20px rgba(255, 0, 0, 0.3);
        }

        .hamburger {
            display: none;
            flex-direction: column;
            cursor: pointer;
            gap: 5px;
        }

        .hamburger span {
            width: 25px;
            height: 3px;
            background: var(--text-dark);
            border-radius: 2px;
            transition: all 0.3s ease;
        }

        nav.dark-bg .hamburger span {
            background: var(--text-light);
        }

        .hamburger.active span:nth-child(1) {
            transform: rotate(45deg) translate(10px, 10px);
        }

        .hamburger.active span:nth-child(2) {
            opacity: 0;
        }

        .hamburger.active span:nth-child(3) {
            transform: rotate(-45deg) translate(7px, -7px);
        }

        /* ==================== HERO SECTION ==================== */
        .hero {
            min-height: 100vh;
            display: flex;
            align-items: center;
            justify-content: center;
            background: linear-gradient(135deg, #0f0f0f 0%, #1a1a1a 100%);
            position: relative;
            overflow: hidden;
            margin-top: 60px;
            padding: 2rem;
        }

        .hero::before {
            content: '';
            position: absolute;
            width: 400px;
            height: 400px;
            background: radial-gradient(circle, rgba(255, 0, 0, 0.3) 0%, transparent 70%);
            border-radius: 50%;
            top: 10%;
            right: 10%;
            animation: float 6s ease-in-out infinite;
        }

        .hero::after {
            content: '';
            position: absolute;
            width: 300px;
            height: 300px;
            background: radial-gradient(circle, rgba(255, 0, 0, 0.2) 0%, transparent 70%);
            border-radius: 50%;
            bottom: 5%;
            left: 5%;
            animation: float 8s ease-in-out infinite reverse;
        }

        @keyframes float {
            0%, 100% { transform: translateY(0px); }
            50% { transform: translateY(-30px); }
        }

        .hero-content {
            position: relative;
            z-index: 2;
            text-align: center;
            max-width: 1000px;
            animation: fadeInUp 1s ease-out;
        }

        .hero-product {
            width: 200px;
            height: 400px;
            margin: 0 auto 3rem;
            position: relative;
            animation: slideInRight 1s ease-out 0.2s backwards;
        }

        .hero-product img {
            width: 100%;
            height: 100%;
            object-fit: contain;
            filter: drop-shadow(0 20px 60px rgba(255, 0, 0, 0.4));
            animation: rotateY 3s ease-in-out infinite;
        }

        @keyframes rotateY {
            0%, 100% { transform: rotateY(0deg) scaleX(1); }
            50% { transform: rotateY(5deg) scaleX(1.02); }
        }

        .hero h1 {
            font-size: clamp(2.5rem, 8vw, 5rem);
            color: var(--text-light);
            font-weight: 900;
            margin-bottom: 1rem;
            letter-spacing: -2px;
            text-transform: uppercase;
            animation: slideInUp 1s ease-out 0.1s backwards;
            line-height: 1.2;
        }

        .hero h1 span {
            color: var(--primary-red);
            display: inline-block;
            animation: scaleIn 0.8s ease-out 0.5s backwards;
        }

        @keyframes scaleIn {
            from { transform: scale(0.5); opacity: 0; }
            to { transform: scale(1); opacity: 1; }
        }

        .hero p {
            font-size: 1.2rem;
            color: rgba(255, 255, 255, 0.8);
            margin-bottom: 2rem;
            animation: slideInUp 1s ease-out 0.2s backwards;
            max-width: 600px;
            margin-left: auto;
            margin-right: auto;
        }

        .hero-buttons {
            display: flex;
            gap: 1rem;
            justify-content: center;
            flex-wrap: wrap;
            animation: slideInUp 1s ease-out 0.3s backwards;
        }

        .btn {
            padding: 1rem 2.5rem;
            font-size: 1rem;
            font-weight: 700;
            border: none;
            border-radius: 50px;
            cursor: pointer;
            transition: all 0.3s ease;
            text-transform: uppercase;
            letter-spacing: 1px;
            position: relative;
            overflow: hidden;
        }

        .btn-primary {
            background: var(--primary-red);
            color: var(--text-light);
        }

        .btn-primary::before {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            background: var(--dark-red);
            transition: left 0.3s ease;
            z-index: -1;
        }

        .btn-primary:hover::before {
            left: 0;
        }

        .btn-primary:hover {
            transform: translateY(-3px);
            box-shadow: 0 15px 35px rgba(255, 0, 0, 0.4);
        }

        .btn-secondary {
            background: transparent;
            color: var(--text-light);
            border: 2px solid var(--text-light);
        }

        .btn-secondary:hover {
            background: var(--text-light);
            color: var(--text-dark);
            transform: translateY(-3px);
            box-shadow: 0 15px 35px rgba(255, 255, 255, 0.2);
        }

        @keyframes fadeInUp {
            from { opacity: 0; transform: translateY(30px); }
            to { opacity: 1; transform: translateY(0); }
        }

        @keyframes slideInRight {
            from { opacity: 0; transform: translateX(50px); }
            to { opacity: 1; transform: translateX(0); }
        }

        @keyframes slideInUp {
            from { opacity: 0; transform: translateY(30px); }
            to { opacity: 1; transform: translateY(0); }
        }

        /* ==================== PRODUCTS SECTION ==================== */
        .products {
            padding: 5rem 2rem;
            background: var(--bg-light);
        }

        .section-title {
            text-align: center;
            margin-bottom: 3rem;
        }

        .section-title h2 {
            font-size: clamp(2rem, 5vw, 3.5rem);
            color: var(--text-dark);
            font-weight: 900;
            margin-bottom: 0.5rem;
            letter-spacing: -1px;
        }

        .section-title .accent {
            color: var(--primary-red);
        }

        .section-title p {
            font-size: 1.1rem;
            color: #666;
            max-width: 500px;
            margin: 0 auto;
        }

        .products-grid {
            max-width: 1400px;
            margin: 0 auto;
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
            gap: 2rem;
        }

        .product-card {
            background: white;
            border-radius: 15px;
            overflow: hidden;
            box-shadow: var(--shadow-md);
            transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1);
            display: flex;
            flex-direction: column;
            cursor: pointer;
            animation: fadeInUp 0.6s ease-out backwards;
        }

        .product-card:nth-child(1) { animation-delay: 0.1s; }
        .product-card:nth-child(2) { animation-delay: 0.2s; }
        .product-card:nth-child(3) { animation-delay: 0.3s; }
        .product-card:nth-child(4) { animation-delay: 0.4s; }
        .product-card:nth-child(5) { animation-delay: 0.5s; }
        .product-card:nth-child(6) { animation-delay: 0.6s; }

        .product-card:hover {
            transform: translateY(-15px);
            box-shadow: 0 25px 50px rgba(255, 0, 0, 0.15);
        }

        .product-image {
            width: 100%;
            height: 280px;
            background: linear-gradient(135deg, #f5f5f5 0%, #e8e8e8 100%);
            display: flex;
            align-items: center;
            justify-content: center;
            position: relative;
            overflow: hidden;
        }

        .product-image img {
            width: 100%;
            height: 100%;
            object-fit: contain;
            transition: transform 0.4s ease;
        }

        .product-card:hover .product-image img {
            transform: scale(1.1) rotate(5deg);
        }

        .product-info {
            padding: 1.5rem;
            flex-grow: 1;
            display: flex;
            flex-direction: column;
        }

        .product-name {
            font-size: 1.3rem;
            font-weight: 700;
            color: var(--text-dark);
            margin-bottom: 0.5rem;
        }

        .product-desc {
            font-size: 0.95rem;
            color: #666;
            margin-bottom: 1.5rem;
            flex-grow: 1;
        }

        .product-button {
            align-self: flex-start;
            background: var(--primary-red);
            color: var(--text-light);
            border: none;
            padding: 0.7rem 1.5rem;
            border-radius: 25px;
            cursor: pointer;
            font-weight: 700;
            font-size: 0.9rem;
            transition: all 0.3s ease;
            text-transform: uppercase;
            letter-spacing: 0.5px;
        }

        .product-button:hover {
            background: var(--dark-red);
            transform: translateX(5px);
        }

        /* ==================== FEATURED DRINK SECTION ==================== */
        .featured {
            padding: 5rem 2rem;
            background: linear-gradient(135deg, #0f0f0f 0%, #1a1a1a 100%);
            color: var(--text-light);
        }

        .featured-container {
            max-width: 1200px;
            margin: 0 auto;
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 3rem;
            align-items: center;
        }

        .featured-image {
            position: relative;
            height: 500px;
            display: flex;
            align-items: center;
            justify-content: center;
        }

        .featured-image::before {
            content: '';
            position: absolute;
            width: 300px;
            height: 300px;
            background: radial-gradient(circle, rgba(255, 0, 0, 0.2) 0%, transparent 70%);
            border-radius: 50%;
            animation: float 4s ease-in-out infinite;
        }

        .featured-image img {
            width: 280px;
            height: 400px;
            object-fit: contain;
            position: relative;
            z-index: 2;
            filter: drop-shadow(0 30px 60px rgba(255, 0, 0, 0.3));
            animation: slideInLeft 0.8s ease-out;
        }

        @keyframes slideInLeft {
            from { opacity: 0; transform: translateX(-50px); }
            to { opacity: 1; transform: translateX(0); }
        }

        .featured-content {
            animation: slideInRight 0.8s ease-out;
        }

        .featured-content h3 {
            font-size: 0.95rem;
            color: var(--primary-red);
            text-transform: uppercase;
            letter-spacing: 2px;
            margin-bottom: 1rem;
            font-weight: 700;
        }

        .featured-content h2 {
            font-size: clamp(2rem, 5vw, 3rem);
            margin-bottom: 1.5rem;
            font-weight: 900;
            line-height: 1.2;
        }

        .featured-content p {
            font-size: 1.1rem;
            color: rgba(255, 255, 255, 0.8);
            margin-bottom: 2rem;
            line-height: 1.6;
        }

        .nutrition-grid {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 1.5rem;
            margin: 2rem 0;
            padding: 2rem 0;
            border-top: 1px solid rgba(255, 255, 255, 0.2);
            border-bottom: 1px solid rgba(255, 255, 255, 0.2);
        }

        .nutrition-item {
            background: rgba(255, 255, 255, 0.05);
            padding: 1.5rem;
            border-radius: 10px;
            border-left: 3px solid var(--primary-red);
        }

        .nutrition-label {
            font-size: 0.85rem;
            color: rgba(255, 255, 255, 0.7);
            text-transform: uppercase;
            letter-spacing: 1px;
            margin-bottom: 0.5rem;
        }

        .nutrition-value {
            font-size: 1.5rem;
            font-weight: 700;
            color: var(--text-light);
        }

        /* ==================== ABOUT SECTION ==================== */
        .about {
            padding: 5rem 2rem;
            background: var(--bg-light);
        }

        .about-container {
            max-width: 1200px;
            margin: 0 auto;
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 3rem;
            align-items: center;
        }

        .about-image {
            height: 400px;
            background: linear-gradient(135deg, var(--primary-red), var(--dark-red));
            border-radius: 15px;
            display: flex;
            align-items: center;
            justify-content: center;
            overflow: hidden;
            box-shadow: var(--shadow-lg);
        }

        .about-image img {
            width: 100%;
            height: 100%;
            object-fit: cover;
        }

        .about-content h2 {
            font-size: clamp(2rem, 5vw, 3rem);
            color: var(--text-dark);
            margin-bottom: 1.5rem;
            font-weight: 900;
        }

        .about-content p {
            font-size: 1.1rem;
            color: #666;
            line-height: 1.8;
            margin-bottom: 1.5rem;
        }

        .about-list {
            list-style: none;
            margin: 2rem 0;
        }

        .about-list li {
            font-size: 1rem;
            color: var(--text-dark);
            padding: 0.8rem 0;
            padding-left: 2rem;
            position: relative;
        }

        .about-list li::before {
            content: '✓';
            position: absolute;
            left: 0;
            color: var(--primary-red);
            font-weight: 700;
            font-size: 1.2rem;
        }

        /* ==================== PROMO VIDEO SECTION ==================== */
        .promo {
            padding: 5rem 2rem;
            background: linear-gradient(135deg, #0f0f0f 0%, #1a1a1a 100%);
            color: var(--text-light);
        }

        .promo-container {
            max-width: 1000px;
            margin: 0 auto;
            text-align: center;
        }

        .promo-video {
            width: 100%;
            aspect-ratio: 16/9;
            background: rgba(255, 0, 0, 0.1);
            border-radius: 15px;
            overflow: hidden;
            margin: 2rem 0;
            box-shadow: 0 30px 60px rgba(255, 0, 0, 0.2);
            display: flex;
            align-items: center;
            justify-content: center;
            cursor: pointer;
            position: relative;
            transition: all 0.3s ease;
        }

        .promo-video:hover {
            box-shadow: 0 40px 80px rgba(255, 0, 0, 0.3);
            transform: scale(1.02);
        }

        .play-button {
            width: 80px;
            height: 80px;
            background: var(--primary-red);
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            color: white;
            font-size: 30px;
            transition: all 0.3s ease;
            animation: pulse-scale 2s ease-in-out infinite;
        }

        @keyframes pulse-scale {
            0%, 100% { transform: scale(1); box-shadow: 0 0 0 0 rgba(255, 0, 0, 0.5); }
            50% { transform: scale(1.05); box-shadow: 0 0 0 20px rgba(255, 0, 0, 0); }
        }

        .promo-video:hover .play-button {
            background: var(--dark-red);
            transform: scale(1.15);
        }

        /* ==================== NEWS SECTION ==================== */
        .news {
            padding: 5rem 2rem;
            background: var(--bg-light);
        }

        .news-grid {
            max-width: 1400px;
            margin: 3rem auto 0;
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 2rem;
        }

        .news-card {
            background: white;
            border-radius: 15px;
            overflow: hidden;
            box-shadow: var(--shadow-md);
            transition: all 0.4s ease;
            display: flex;
            flex-direction: column;
            animation: fadeInUp 0.6s ease-out backwards;
        }

        .news-card:nth-child(1) { animation-delay: 0.1s; }
        .news-card:nth-child(2) { animation-delay: 0.2s; }
        .news-card:nth-child(3) { animation-delay: 0.3s; }

        .news-card:hover {
            transform: translateY(-10px);
            box-shadow: 0 25px 50px rgba(0, 0, 0, 0.1);
        }

        .news-image {
            width: 100%;
            height: 200px;
            background: linear-gradient(135deg, var(--primary-red), var(--dark-red));
            overflow: hidden;
        }

        .news-image img {
            width: 100%;
            height: 100%;
            object-fit: cover;
            transition: transform 0.4s ease;
        }

        .news-card:hover .news-image img {
            transform: scale(1.1);
        }

        .news-body {
            padding: 1.5rem;
            flex-grow: 1;
            display: flex;
            flex-direction: column;
        }

        .news-date {
            font-size: 0.85rem;
            color: var(--primary-red);
            font-weight: 700;
            text-transform: uppercase;
            letter-spacing: 1px;
            margin-bottom: 0.5rem;
        }

        .news-title {
            font-size: 1.3rem;
            color: var(--text-dark);
            font-weight: 700;
            margin-bottom: 0.8rem;
        }

        .news-excerpt {
            font-size: 0.95rem;
            color: #666;
            line-height: 1.6;
            flex-grow: 1;
            margin-bottom: 1rem;
        }

        .news-link {
            color: var(--primary-red);
            text-decoration: none;
            font-weight: 700;
            text-transform: uppercase;
            font-size: 0.85rem;
            letter-spacing: 1px;
            transition: all 0.3s ease;
            display: inline-block;
        }

        .news-link:hover {
            color: var(--dark-red);
            transform: translateX(5px);
        }

        /* ==================== NEWSLETTER SECTION ==================== */
        .newsletter {
            padding: 4rem 2rem;
            background: linear-gradient(135deg, var(--primary-red), var(--dark-red));
            color: var(--text-light);
            text-align: center;
        }

        .newsletter-container {
            max-width: 600px;
            margin: 0 auto;
        }

        .newsletter h2 {
            font-size: clamp(1.8rem, 5vw, 2.5rem);
            margin-bottom: 1rem;
            font-weight: 900;
        }

        .newsletter p {
            font-size: 1.1rem;
            margin-bottom: 2rem;
            opacity: 0.95;
        }

        .form-group {
            display: flex;
            gap: 0.5rem;
            margin-bottom: 1rem;
        }

        .form-group input {
            flex-grow: 1;
            padding: 1rem;
            border: none;
            border-radius: 50px;
            font-size: 1rem;
            outline: none;
            transition: all 0.3s ease;
        }

        .form-group input:focus {
            box-shadow: 0 0 20px rgba(255, 255, 255, 0.3);
        }

        .form-group button {
            padding: 1rem 2rem;
            background: rgba(255, 255, 255, 0.2);
            color: var(--text-light);
            border: 2px solid white;
            border-radius: 50px;
            cursor: pointer;
            font-weight: 700;
            text-transform: uppercase;
            letter-spacing: 1px;
            transition: all 0.3s ease;
            font-size: 0.9rem;
        }

        .form-group button:hover {
            background: white;
            color: var(--primary-red);
            transform: translateY(-2px);
        }

        .newsletter-message {
            font-size: 0.95rem;
            color: rgba(255, 255, 255, 0.8);
            margin-top: 1rem;
        }

        /* ==================== FOOTER ==================== */
        footer {
            background: var(--bg-dark);
            color: var(--text-light);
            padding: 3rem 2rem 1rem;
        }

        .footer-content {
            max-width: 1400px;
            margin: 0 auto;
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 2rem;
            margin-bottom: 2rem;
        }

        .footer-section h3 {
            font-size: 1.1rem;
            margin-bottom: 1rem;
            color: var(--primary-red);
            font-weight: 700;
            text-transform: uppercase;
            letter-spacing: 1px;
        }

        .footer-section a,
        .footer-section p {
            color: rgba(255, 255, 255, 0.7);
            text-decoration: none;
            font-size: 0.95rem;
            margin-bottom: 0.5rem;
            transition: all 0.3s ease;
            display: inline-block;
        }

        .footer-section a:hover {
            color: var(--primary-red);
            transform: translateX(5px);
        }

        .social-links {
            display: flex;
            gap: 1rem;
        }

        .social-links a {
            width: 40px;
            height: 40px;
            background: rgba(255, 255, 255, 0.1);
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            transition: all 0.3s ease;
            margin-bottom: 0;
        }

        .social-links a:hover {
            background: var(--primary-red);
            transform: translateY(-3px) scale(1.1);
        }

        .footer-bottom {
            border-top: 1px solid rgba(255, 255, 255, 0.1);
            padding-top: 2rem;
            text-align: center;
            color: rgba(255, 255, 255, 0.6);
            font-size: 0.9rem;
        }

        /* ==================== SCROLL TO TOP BUTTON ==================== */
        .scroll-to-top {
            position: fixed;
            bottom: 30px;
            right: 30px;
            width: 50px;
            height: 50px;
            background: var(--primary-red);
            color: white;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            cursor: pointer;
            font-size: 24px;
            opacity: 0;
            visibility: hidden;
            transition: all 0.3s ease;
            z-index: 500;
            box-shadow: var(--shadow-lg);
        }

        .scroll-to-top.visible {
            opacity: 1;
            visibility: visible;
        }

        .scroll-to-top:hover {
            background: var(--dark-red);
            transform: translateY(-5px);
            box-shadow: 0 15px 35px rgba(255, 0, 0, 0.4);
        }

        /* ==================== RESPONSIVE DESIGN ==================== */
        @media (max-width: 768px) {
            .nav-menu {
                display: none;
                position: absolute;
                top: 70px;
                left: 0;
                width: 100%;
                background: rgba(255, 255, 255, 0.98);
                flex-direction: column;
                gap: 0.5rem;
                padding: 2rem;
                z-index: 999;
            }

            .nav-menu.active {
                display: flex;
            }

            .nav-menu a {
                font-size: 1.1rem;
                padding: 1rem;
            }

            .hamburger {
                display: flex;
            }

            .hero {
                margin-top: 70px;
                padding: 2rem 1rem;
            }

            .hero-product {
                width: 150px;
                height: 300px;
            }

            .featured-container,
            .about-container {
                grid-template-columns: 1fr;
                gap: 2rem;
            }

            .featured-image {
                height: 350px;
            }

            .featured-image img {
                width: 200px;
                height: 300px;
            }

            .nutrition-grid {
                grid-template-columns: 1fr;
            }

            .hero-buttons {
                flex-direction: column;
            }

            .btn {
                width: 100%;
            }

            .scroll-to-top {
                bottom: 20px;
                right: 20px;
                width: 45px;
                height: 45px;
                font-size: 20px;
            }

            nav.scrolled {
                padding: 0.5rem 1rem;
            }

            .logo {
                font-size: 24px;
            }
        }

        @media (max-width: 480px) {
            .products-grid,
            .news-grid {
                grid-template-columns: 1fr;
            }

            .hero h1 {
                font-size: 2rem;
            }

            .section-title h2 {
                font-size: 1.8rem;
            }

            .featured-content h2 {
                font-size: 1.8rem;
            }

            .about-content h2 {
                font-size: 1.8rem;
            }

            .newsletter h2 {
                font-size: 1.5rem;
            }

            .form-group {
                flex-direction: column;
            }

            .form-group button {
                padding: 0.8rem 1.5rem;
            }

            .nav-container {
                gap: 1rem;
            }

            .nav-cta {
                padding: 0.6rem 1rem;
                font-size: 11px;
            }
        }
    </style>
</head>
<body>
    <!-- LOADING ANIMATION -->
    <div class="loader">
        <div class="loader-content">
            <div class="loader-circle"></div>
            <div class="loader-text">Opening Happiness</div>
        </div>
    </div>

    <!-- NAVIGATION -->
    <nav id="navbar">
        <div class="nav-container">
            <div class="logo">🥤 Coca-Cola</div>
            <ul class="nav-menu" id="navMenu">
                <li><a href="#hero" class="nav-link active">Home</a></li>
                <li><a href="#products" class="nav-link">Products</a></li>
                <li><a href="#featured" class="nav-link">Featured</a></li>
                <li><a href="#about" class="nav-link">About</a></li>
                <li><a href="#news" class="nav-link">News</a></li>
            </ul>
            <button class="nav-cta">Contact Us</button>
            <div class="hamburger" id="hamburger">
                <span></span>
                <span></span>
                <span></span>
            </div>
        </div>
    </nav>

    <!-- HERO SECTION -->
    <section class="hero" id="hero">
        <div class="hero-content">
            <div class="hero-product">
                <img src="data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 200 400'%3E%3Cdefs%3E%3ClinearGradient id='cola' x1='0%' y1='0%' x2='0%' y2='100%'%3E%3Cstop offset='0%' style='stop-color:%23FF0000;stop-opacity:1' /%3E%3Cstop offset='50%' style='stop-color:%23CC0000;stop-opacity:1' /%3E%3Cstop offset='100%' style='stop-color:%23990000;stop-opacity:1' /%3E%3C/linearGradient%3E%3C/defs%3E%3Crect x='30' y='20' width='140' height='200' rx='15' fill='url(%23cola)' /%3E%3Cellipse cx='100' cy='20' rx='70' ry='15' fill='%23ffffff' opacity='0.3' /%3E%3Ctext x='100' y='130' font-family='Arial, sans-serif' font-size='32' font-weight='bold' fill='%23ffffff' text-anchor='middle' letter-spacing='2'%3ECOCA%3C/text%3E%3Ctext x='100' y='165' font-family='Arial, sans-serif' font-size='28' fill='%23ffffff' text-anchor='middle' letter-spacing='1'%3ECOLA%3C/text%3E%3Ccircle cx='50' cy='100' r='8' fill='%23ffffff' opacity='0.4' /%3E%3Ccircle cx='150' cy='150' r='6' fill='%23ffffff' opacity='0.3' /%3E%3Ccircle cx='80' cy='200' r='5' fill='%23ffffff' opacity='0.25' /%3E%3C/svg%3E" alt="Coca-Cola Bottle">
            </div>
            <h1>Open <span>Happiness</span></h1>
            <p>Taste the magic of the world's most iconic beverage. Experience refreshment like never before.</p>
            <div class="hero-buttons">
                <button class="btn btn-primary" onclick="scrollToSection('#products')">Explore Drinks</button>
                <button class="btn btn-secondary" onclick="scrollToSection('#featured')">Shop Now</button>
            </div>
        </div>
    </section>

    <!-- PRODUCTS SECTION -->
    <section class="products" id="products">
        <div class="section-title">
            <h2>Discover Our <span class="accent">Collection</span></h2>
            <p>From classic favorites to innovative new flavors</p>
        </div>
        <div class="products-grid">
            <div class="product-card">
                <div class="product-image">
                    <img src="data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 150 250'%3E%3ClinearGradient id='g1' x1='0%' y1='0%' x2='0%' y2='100%'%3E%3Cstop offset='0%' style='stop-color:%23FF0000'/%3E%3Cstop offset='100%' style='stop-color:%23CC0000'/%3E%3C/linearGradient%3E%3Crect x='20' y='10' width='110' height='150' rx='10' fill='url(%23g1)'/%3E%3Ctext x='75' y='95' font-family='Arial' font-size='24' font-weight='bold' fill='white' text-anchor='middle'%3ECOCA%3C/text%3E%3Crect x='30' y='170' width='90' height='50' rx='8' fill='%23999' opacity='0.3'/%3E%3C/svg%3E" alt="Coca-Cola Classic">
                </div>
                <div class="product-info">
                    <h3 class="product-name">Coca-Cola Classic</h3>
                    <p class="product-desc">The original taste that's refreshed generations. The perfect balance of flavor and fizz.</p>
                    <button class="product-button">View Details</button>
                </div>
            </div>

            <div class="product-card">
                <div class="product-image">
                    <img src="data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 150 250'%3E%3ClinearGradient id='g2' x1='0%' y1='0%' x2='0%' y2='100%'%3E%3Cstop offset='0%' style='stop-color:%23000000'/%3E%3Cstop offset='100%' style='stop-color:%23333333'/%3E%3C/linearGradient%3E%3Crect x='20' y='10' width='110' height='150' rx='10' fill='url(%23g2)'/%3E%3Ctext x='75' y='80' font-family='Arial' font-size='16' font-weight='bold' fill='white' text-anchor='middle'%3ECOCA%3C/text%3E%3Ctext x='75' y='105' font-family='Arial' font-size='16' fill='white' text-anchor='middle'%3EZERO%3C/text%3E%3Crect x='30' y='170' width='90' height='50' rx='8' fill='%23999' opacity='0.3'/%3E%3C/svg%3E" alt="Coca-Cola Zero Sugar">
                </div>
                <div class="product-info">
                    <h3 class="product-name">Coca-Cola Zero Sugar</h3>
                    <p class="product-desc">Zero sugar, maximum taste. Enjoy the real Coca-Cola flavor with none of the guilt.</p>
                    <button class="product-button">View Details</button>
                </div>
            </div>

            <div class="product-card">
                <div class="product-image">
                    <img src="data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 150 250'%3E%3ClinearGradient id='g3' x1='0%' y1='0%' x2='0%' y2='100%'%3E%3Cstop offset='0%' style='stop-color:%238B0000'/%3E%3Cstop offset='100%' style='stop-color:%23660000'/%3E%3C/linearGradient%3E%3Crect x='20' y='10' width='110' height='150' rx='10' fill='url(%23g3)'/%3E%3Ctext x='75' y='95' font-family='Arial' font-size='18' font-weight='bold' fill='white' text-anchor='middle'%3ECHERRYPOP%3C/text%3E%3Crect x='30' y='170' width='90' height='50' rx='8' fill='%23999' opacity='0.3'/%3E%3C/svg%3E" alt="Coca-Cola Cherry">
                </div>
                <div class="product-info">
                    <h3 class="product-name">Coca-Cola Cherry Pop</h3>
                    <p class="product-desc">Sweet cherry flavor meets crisp cola. A burst of fruity freshness in every sip.</p>
                    <button class="product-button">View Details</button>
                </div>
            </div>

            <div class="product-card">
                <div class="product-image">
                    <img src="data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 150 250'%3E%3ClinearGradient id='g4' x1='0%' y1='0%' x2='0%' y2='100%'%3E%3Cstop offset='0%' style='stop-color:%23FF6B9D'/%3E%3Cstop offset='100%' style='stop-color:%23FF0040'/%3E%3C/linearGradient%3E%3Crect x='20' y='10' width='110' height='150' rx='10' fill='url(%23g4)'/%3E%3Ctext x='75' y='95' font-family='Arial' font-size='16' font-weight='bold' fill='white' text-anchor='middle'%3EVIZ%3C/text%3E%3Crect x='30' y='170' width='90' height='50' rx='8' fill='%23999' opacity='0.3'/%3E%3C/svg%3E" alt="Coca-Cola Viz">
                </div>
                <div class="product-info">
                    <h3 class="product-name">Coca-Cola Viz</h3>
                    <p class="product-desc">Bold, vibrant, and unapologetically pink. The taste of pure tropical energy.</p>
                    <button class="product-button">View Details</button>
                </div>
            </div>

            <div class="product-card">
                <div class="product-image">
                    <img src="data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 150 250'%3E%3ClinearGradient id='g5' x1='0%' y1='0%' x2='0%' y2='100%'%3E%3Cstop offset='0%' style='stop-color:%23FF8C00'/%3E%3Cstop offset='100%' style='stop-color:%23FF6500'/%3E%3C/linearGradient%3E%3Crect x='20' y='10' width='110' height='150' rx='10' fill='url(%23g5)'/%3E%3Ctext x='75' y='80' font-family='Arial' font-size='14' font-weight='bold' fill='white' text-anchor='middle'%3ECOCA%3C/text%3E%3Ctext x='75' y='105' font-family='Arial' font-size='14' fill='white' text-anchor='middle'%3EORANGE%3C/text%3E%3Crect x='30' y='170' width='90' height='50' rx='8' fill='%23999' opacity='0.3'/%3E%3C/svg%3E" alt="Coca-Cola Orange">
                </div>
                <div class="product-info">
                    <h3 class="product-name">Coca-Cola Orange</h3>
                    <p class="product-desc">Citrus sunshine in a bottle. Refreshingly bold orange taste with iconic cola flavor.</p>
                    <button class="product-button">View Details</button>
                </div>
            </div>

            <div class="product-card">
                <div class="product-image">
                    <img src="data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 150 250'%3E%3ClinearGradient id='g6' x1='0%' y1='0%' x2='0%' y2='100%'%3E%3Cstop offset='0%' style='stop-color:%2300AA77'/%3E%3Cstop offset='100%' style='stop-color:%23008855'/%3E%3C/linearGradient%3E%3Crect x='20' y='10' width='110' height='150' rx='10' fill='url(%23g6)'/%3E%3Ctext x='75' y='80' font-family='Arial' font-size='14' font-weight='bold' fill='white' text-anchor='middle'%3ECOCA%3C/text%3E%3Ctext x='75' y='105' font-family='Arial' font-size='14' fill='white' text-anchor='middle'%3ELIME%3C/text%3E%3Crect x='30' y='170' width='90' height='50' rx='8' fill='%23999' opacity='0.3'/%3E%3C/svg%3E" alt="Coca-Cola Lime">
                </div>
                <div class="product-info">
                    <h3 class="product-name">Coca-Cola Lime</h3>
                    <p class="product-desc">Zesty lime twist on a classic favorite. Crisp, tangy, and absolutely refreshing.</p>
                    <button class="product-button">View Details</button>
                </div>
            </div>
        </div>
    </section>

    <!-- FEATURED DRINK SECTION -->
    <section class="featured" id="featured">
        <div class="featured-container">
            <div class="featured-image">
                <img src="data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 200 400'%3E%3Cdefs%3E%3ClinearGradient id='cola2' x1='0%' y1='0%' x2='0%' y2='100%'%3E%3Cstop offset='0%' style='stop-color:%23000000;stop-opacity:1' /%3E%3Cstop offset='50%' style='stop-color:%23333333;stop-opacity:1' /%3E%3Cstop offset='100%' style='stop-color:%23111111;stop-opacity:1' /%3E%3C/linearGradient%3E%3C/defs%3E%3Crect x='30' y='20' width='140' height='200' rx='15' fill='url(%23cola2)' /%3E%3Cellipse cx='100' cy='20' rx='70' ry='15' fill='%23ffffff' opacity='0.2' /%3E%3Ctext x='100' y='120' font-family='Arial' font-size='24' font-weight='bold' fill='%23ffffff' text-anchor='middle'%3ECOCA%3C/text%3E%3Ctext x='100' y='150' font-family='Arial' font-size='24' fill='%23ffffff' text-anchor='middle'%3EZERO%3C/text%3E%3Ccircle cx='50' cy='100' r='8' fill='%23ffffff' opacity='0.3' /%3E%3Ccircle cx='150' cy='150' r='6' fill='%23ffffff' opacity='0.2' /%3E%3C/svg%3E" alt="Coca-Cola Zero Sugar">
            </div>
            <div class="featured-content">
                <h3>Featured Product</h3>
                <h2>Coca-Cola Zero Sugar</h2>
                <p>Experience the uncompromising taste of Coca-Cola with zero sugar. No artificial aftertaste, just pure, refreshing cola perfection. Perfect for those who refuse to compromise on taste or their health goals.</p>
                
                <div class="nutrition-grid">
                    <div class="nutrition-item">
                        <div class="nutrition-label">Calories</div>
                        <div class="nutrition-value">0</div>
                    </div>
                    <div class="nutrition-item">
                        <div class="nutrition-label">Sugar</div>
                        <div class="nutrition-value">0g</div>
                    </div>
                    <div class="nutrition-item">
                        <div class="nutrition-label">Sodium</div>
                        <div class="nutrition-value">40mg</div>
                    </div>
                    <div class="nutrition-item">
                        <div class="nutrition-label">Caffeine</div>
                        <div class="nutrition-value">34mg</div>
                    </div>
                </div>

                <button class="btn btn-primary">Learn More & Shop</button>
            </div>
        </div>
    </section>

    <!-- ABOUT SECTION -->
    <section class="about" id="about">
        <div class="about-container">
            <div class="about-image">
                <img src="data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 400 300'%3E%3Crect width='400' height='300' fill='%23FF0000'/%3E%3Ctext x='200' y='150' font-family='Arial' font-size='48' font-weight='bold' fill='white' text-anchor='middle' dominant-baseline='middle'%3EEnjoy%3C/text%3E%3Ctext x='200' y='200' font-family='Arial' font-size='36' fill='white' text-anchor='middle' dominant-baseline='middle'%3EHappiness%3C/text%3E%3C/svg%3E" alt="Brand Story">
            </div>
            <div class="about-content">
                <h2>Our <span class="accent">Story</span></h2>
                <p>Founded in 1886, Coca-Cola has been the world's most refreshing beverage, bringing moments of happiness to billions of people across the globe. Our commitment to quality, innovation, and taste has made us a household name.</p>
                <p>We believe in the power of connection. Every bottle of Coca-Cola is an invitation to pause, refresh, and enjoy life's moments—whether big or small. From family gatherings to celebrations with friends, we're there to add that perfect touch of happiness.</p>
                
                <ul class="about-list">
                    <li>Premium quality ingredients sourced responsibly</li>
                    <li>Innovative flavors that delight taste buds</li>
                    <li>Sustainable packaging and eco-friendly practices</li>
                    <li>Commitment to global communities and diversity</li>
                    <li>Continuous innovation in taste and nutrition</li>
                </ul>
            </div>
        </div>
    </section>

    <!-- PROMO VIDEO SECTION -->
    <section class="promo" id="promo">
        <div class="promo-container">
            <div class="section-title">
                <h2 style="color: white;">Watch Our <span class="accent">Latest Campaign</span></h2>
                <p style="color: rgba(255,255,255,0.8);">See what happiness looks like</p>
            </div>
            <div class="promo-video">
                <div class="play-button">▶</div>
            </div>
        </div>
    </section>

    <!-- NEWS SECTION -->
    <section class="news" id="news">
        <div class="section-title">
            <h2>Latest <span class="accent">News</span></h2>
            <p>Stay updated with our newest releases and campaigns</p>
        </div>
        <div class="news-grid">
            <div class="news-card">
                <div class="news-image">
                    <img src="data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 300 200'%3E%3Crect width='300' height='200' fill='%23FF0000'/%3E%3Ctext x='150' y='100' font-family='Arial' font-size='24' font-weight='bold' fill='white' text-anchor='middle' dominant-baseline='middle'%3ENEW FLAVOR%3C/text%3E%3C/svg%3E" alt="New Flavor">
                </div>
                <div class="news-body">
                    <div class="news-date">April 2024</div>
                    <h3 class="news-title">Revolutionary New Flavor Launch</h3>
                    <p class="news-excerpt">Introducing Coca-Cola Cosmic Cherry, our boldest flavor yet. A blend of cherry, vanilla, and cosmic energy that's out of this world.</p>
                    <a href="#" class="news-link">Read More →</a>
                </div>
            </div>

            <div class="news-card">
                <div class="news-image">
                    <img src="data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 300 200'%3E%3Crect width='300' height='200' fill='%23FF6B9D'/%3E%3Ctext x='150' y='100' font-family='Arial' font-size='24' font-weight='bold' fill='white' text-anchor='middle' dominant-baseline='middle'%3ESUSTAINABILITY%3C/text%3E%3C/svg%3E" alt="Sustainability">
                </div>
                <div class="news-body">
                    <div class="news-date">March 2024</div>
                    <h3 class="news-title">Eco-Friendly Packaging Update</h3>
                    <p class="news-excerpt">We're committed to the planet. Our new recycled plastic bottles reduce environmental impact while maintaining premium quality and taste.</p>
                    <a href="#" class="news-link">Read More →</a>
                </div>
            </div>

            <div class="news-card">
                <div class="news-image">
                    <img src="data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 300 200'%3E%3Crect width='300' height='200' fill='%23333333'/%3E%3Ctext x='150' y='100' font-family='Arial' font-size='24' font-weight='bold' fill='white' text-anchor='middle' dominant-baseline='middle'%3ECOMMUNITY%3C/text%3E%3C/svg%3E" alt="Community">
                </div>
                <div class="news-body">
                    <div class="news-date">February 2024</div>
                    <h3 class="news-title">Global Happiness Initiative</h3>
                    <p class="news-excerpt">Joining communities worldwide to spread joy, create opportunities, and make a positive difference in the lives of millions.</p>
                    <a href="#" class="news-link">Read More →</a>
                </div>
            </div>
        </div>
    </section>

    <!-- NEWSLETTER SECTION -->
    <section class="newsletter" id="newsletter">
        <div class="newsletter-container">
            <h2>Stay In The Loop</h2>
            <p>Get exclusive offers, new flavors, and happiness delivered to your inbox</p>
            <form class="form-group" onsubmit="handleSubmit(event)">
                <input type="email" placeholder="Your email address" required>
                <button type="submit">Subscribe</button>
            </form>
            <div class="newsletter-message" id="newsletterMsg"></div>
        </div>
    </section>

    <!-- FOOTER -->
    <footer>
        <div class="footer-content">
            <div class="footer-section">
                <h3>About</h3>
                <p>Your happiness is our mission. Since 1886, refreshing the world.</p>
                <div class="social-links">
                    <a href="#" title="Facebook">f</a>
                    <a href="#" title="Twitter">𝕏</a>
                    <a href="#" title="Instagram">📷</a>
                    <a href="#" title="YouTube">▶</a>
                </div>
            </div>

            <div class="footer-section">
                <h3>Products</h3>
                <a href="#">Coca-Cola Classic</a>
                <a href="#">Coca-Cola Zero</a>
                <a href="#">Coca-Cola Cherry</a>
                <a href="#">Diet Coca-Cola</a>
                <a href="#">Coca-Cola Flavors</a>
            </div>

            <div class="footer-section">
                <h3>Company</h3>
                <a href="#">About Us</a>
                <a href="#">Careers</a>
                <a href="#">Sustainability</a>
                <a href="#">Press</a>
                <a href="#">Contact</a>
            </div>

            <div class="footer-section">
                <h3>Support</h3>
                <a href="#">Help Center</a>
                <a href="#">Privacy Policy</a>
                <a href="#">Terms of Service</a>
                <a href="#">Accessibility</a>
                <a href="#">Cookie Policy</a>
            </div>
        </div>

        <div class="footer-bottom">
            <p>&copy; 2024 The Coca-Cola Company. All rights reserved. | Crafted with ❤️ | Open Happiness</p>
        </div>
    </footer>

    <!-- SCROLL TO TOP BUTTON -->
    <button class="scroll-to-top" id="scrollToTop">↑</button>

    <!-- JAVASCRIPT -->
    <script>
        // ==================== NAVIGATION & SCROLL ==================== 
        const navbar = document.getElementById('navbar');
        const navMenu = document.getElementById('navMenu');
        const hamburger = document.getElementById('hamburger');
        const navLinks = document.querySelectorAll('.nav-link');
        const scrollToTopBtn = document.getElementById('scrollToTop');

        // Mobile menu toggle
        hamburger.addEventListener('click', () => {
            hamburger.classList.toggle('active');
            navMenu.classList.toggle('active');
        });

        // Close menu when clicking on a link
        navLinks.forEach(link => {
            link.addEventListener('click', () => {
                hamburger.classList.remove('active');
                navMenu.classList.remove('active');
            });
        });

        // Update active nav link based on scroll
        window.addEventListener('scroll', () => {
            const scrollY = window.scrollY;

            // Navbar scroll effect
            if (scrollY > 50) {
                navbar.classList.add('scrolled');
            } else {
                navbar.classList.remove('scrolled');
            }

            // Hero section styling
            const heroSection = document.getElementById('hero');
            if (scrollY > window.innerHeight / 2) {
                navbar.classList.add('dark-bg');
            } else {
                navbar.classList.remove('dark-bg');
            }

            // Scroll to top button
            if (scrollY > 300) {
                scrollToTopBtn.classList.add('visible');
            } else {
                scrollToTopBtn.classList.remove('visible');
            }

            // Update active nav link
            updateActiveNavLink(scrollY);
        });

        function updateActiveNavLink(scrollY) {
            const sections = ['hero', 'products', 'featured', 'about', 'news'];
            let currentSection = 'hero';

            sections.forEach(section => {
                const element = document.getElementById(section);
                if (element && scrollY >= element.offsetTop - 150) {
                    currentSection = section;
                }
            });

            navLinks.forEach(link => {
                link.classList.remove('active');
                if (link.getAttribute('href') === `#${currentSection}`) {
                    link.classList.add('active');
                }
            });
        }

        // Scroll to top button functionality
        scrollToTopBtn.addEventListener('click', () => {
            window.scrollTo({ top: 0, behavior: 'smooth' });
        });

        // ==================== SCROLL TO SECTION ==================== 
        function scrollToSection(selector) {
            const element = document.querySelector(selector);
            if (element) {
                element.scrollIntoView({ behavior: 'smooth' });
            }
        }

        // ==================== NEWSLETTER FORM ==================== 
        function handleSubmit(event) {
            event.preventDefault();
            const form = event.target;
            const email = form.querySelector('input[type="email"]').value;
            const msgDiv = document.getElementById('newsletterMsg');
            
            msgDiv.textContent = '✓ Thank you! Check your email for exclusive offers.';
            msgDiv.style.color = '#ffffff';
            
            form.reset();
            setTimeout(() => {
                msgDiv.textContent = '';
            }, 3000);
        }

        // ==================== PROMO VIDEO ==================== 
        document.querySelector('.promo-video').addEventListener('click', () => {
            alert('🎬 Video player would open here. Full video: "Open Happiness Campaign 2024"');
        });

        // ==================== PRODUCT BUTTON CLICKS ==================== 
        document.querySelectorAll('.product-button').forEach(button => {
            button.addEventListener('click', (e) => {
                e.target.textContent = '✓ Added to Cart';
                e.target.style.background = '#00aa00';
                setTimeout(() => {
                    e.target.textContent = 'View Details';
                    e.target.style.background = '';
                }, 2000);
            });
        });

        // ==================== SMOOTH SCROLL BEHAVIOR ==================== 
        document.addEventListener('DOMContentLoaded', () => {
            // Animate elements on scroll
            const observerOptions = {
                threshold: 0.1,
                rootMargin: '0px 0px -50px 0px'
            };

            const observer = new IntersectionObserver((entries) => {
                entries.forEach(entry => {
                    if (entry.isIntersecting) {
                        entry.target.style.animation = 'fadeInUp 0.6s ease-out forwards';
                        observer.unobserve(entry.target);
                    }
                });
            }, observerOptions);

            // Optional: observe specific elements if needed
        });

        // ==================== PARALLAX EFFECT ==================== 
        window.addEventListener('scroll', () => {
            const heroSection = document.querySelector('.hero');
            if (heroSection && window.scrollY < window.innerHeight) {
                const offset = window.scrollY * 0.5;
                heroSection.style.backgroundPosition = `0% ${offset}px`;
            }
        });

        // ==================== BUTTON CTA CLICKS ==================== 
        document.querySelector('.nav-cta').addEventListener('click', () => {
            alert('📞 Contact form would open here or navigate to contact page.');
        });

        document.querySelectorAll('.btn-primary').forEach(button => {
            button.addEventListener('mouseenter', function() {
                this.style.letterSpacing = '2px';
            });
            button.addEventListener('mouseleave', function() {
                this.style.letterSpacing = '1px';
            });
        });
    </script>
</body>
</html>
