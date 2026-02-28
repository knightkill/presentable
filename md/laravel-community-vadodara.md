---
marp: true
theme: default
size: 16:9
paginate: false
style: |
  @import url("https://fonts.googleapis.com/css2?family=Manrope:wght@400;500;600;700;800&family=Sora:wght@600;700;800&display=swap");

  html, body, .bespoke-marp-parent {
    background: #dddddd !important;
  }

  section {
    position: relative;
    overflow: hidden;
    padding: 0;
    color: #ffffff;
    font-family: "Manrope", Arial, sans-serif;
    background-image: url("assets/laravel-community-vadodara/bg-base.png"), url("assets/laravel-community-vadodara/bg-pattern.png");
    background-size: cover, cover;
    background-position: center, center;
    background-repeat: no-repeat, no-repeat;
  }
  h1, h2, .intro-title, .content-title, .commitment-title, .thanks {
    font-family: "Sora", Arial, sans-serif;
  }
  .logo-left {
    position: absolute;
    left: 2.5%;
    top: 4.4%;
    width: 15.1%;
  }
  .logo-right {
    position: absolute;
    left: 84.6%;
    top: 7.2%;
    width: 12.9%;
  }
  .hero-community-connect {
    position: absolute;
    left: 17.5%;
    top: 31.2%;
    width: 65.0%;
  }
  .panel-black {
    position: absolute;
    left: 2.5%;
    top: 19.1%;
    width: 95.0%;
    height: 75.7%;
  }
  .panel-purple-left {
    position: absolute;
    left: 2.5%;
    top: 19.1%;
    width: 52.7%;
    height: 62.5%;
  }
  .logo-laravel {
    position: absolute;
    left: 56.3%;
    top: 19.1%;
    width: 41.2%;
    height: 62.5%;
  }
  .panel-purple-large {
    position: absolute;
    left: 2.5%;
    top: 19.1%;
    width: 95.0%;
    height: 62.2%;
  }
  .footer-pill {
    position: absolute;
    left: 2.5%;
    top: 83.5%;
    width: 95.0%;
  }
  .footer-dot {
    position: absolute;
    left: 4.4%;
    top: 87.6%;
    width: 1.8%;
  }
  .footer-date {
    position: absolute;
    left: 6.5%;
    top: 87.0%;
    margin: 0;
    color: #000000;
    font-size: 24px;
    font-weight: 700;
  }
  .intro-title {
    position: absolute;
    left: 4.4%;
    top: 22.4%;
    width: 50.0%;
    margin: 0;
    color: #ffffff;
    font-size: 74px;
    font-weight: 700;
    line-height: 1.03;
  }
  .intro-subtitle {
    position: absolute;
    left: 4.4%;
    top: 57.8%;
    width: 48.8%;
    margin: 0;
    color: #ffffff;
    font-size: 39px;
    line-height: 1.28;
  }
  .content-title {
    position: absolute;
    left: 4.4%;
    top: 25.9%;
    width: 90.0%;
    margin: 0;
    color: #ffffff;
    font-size: 68px;
    font-weight: 700;
    line-height: 1.04;
  }
  .content-list {
    position: absolute;
    left: 4.4%;
    top: 43.6%;
    width: 90.4%;
    margin: 0;
    padding-left: 1.1em;
    list-style: disc;
    color: #ffffff;
    font-size: 33px;
    line-height: 1.28;
  }
  .content-list--tight {
    font-size: 31px;
    line-height: 1.2;
  }
  .commitment-left {
    position: absolute;
    left: 6.0%;
    top: 26.8%;
    width: 32.8%;
    margin: 0;
    color: #ffffff;
    font-size: 32px;
    font-weight: 700;
    line-height: 1.18;
  }
  .commitment-right {
    position: absolute;
    left: 71.9%;
    top: 26.8%;
    width: 24.6%;
    margin: 0;
    color: #ffffff;
    font-size: 32px;
    font-weight: 700;
    line-height: 1.18;
  }
  .commitment-title {
    position: absolute;
    left: 28.1%;
    top: 43.5%;
    width: 43.8%;
    margin: 0;
    color: #ffffff;
    font-size: 68px;
    font-weight: 700;
    line-height: 1.04;
    text-align: center;
  }
  .commitment-center {
    position: absolute;
    left: 40.9%;
    top: 61.6%;
    width: 24.8%;
    margin: 0;
    color: #ffffff;
    font-size: 28px;
    font-weight: 700;
    line-height: 1.25;
    text-align: left;
  }
  .thanks {
    position: absolute;
    left: 13.1%;
    top: 41.3%;
    width: 73.7%;
    margin: 0;
    color: #7f00ff;
    font-size: 160px;
    font-weight: 700;
    line-height: 1.0;
    text-align: center;
  }
  .mobile-hint {
    display: none;
  }

  @media (max-aspect-ratio: 10/16) {
    .logo-left {
      width: 18%;
      top: 3.6%;
      left: 2.3%;
    }
    .logo-right {
      width: 15%;
      top: 3.8%;
      left: 82.0%;
    }
    .footer-pill,
    .footer-dot,
    .footer-date {
      display: none;
    }
    .panel-black,
    .panel-purple-left,
    .logo-laravel,
    .panel-purple-large {
      top: 11%;
      height: 78%;
    }
    .intro-title {
      top: 16%;
      width: 55%;
      font-size: 79px;
      line-height: 1.02;
    }
    .intro-subtitle {
      top: 52%;
      width: 52%;
      font-size: 41px;
      line-height: 1.24;
    }
    .content-title {
      top: 16.5%;
      font-size: 73px;
      line-height: 1.03;
    }
    .content-list {
      top: 40%;
      width: 91.5%;
      font-size: 37px;
      line-height: 1.23;
    }
    .content-list--tight {
      font-size: 34px;
      line-height: 1.15;
    }
    .commitment-left,
    .commitment-right {
      font-size: 34px;
      line-height: 1.16;
    }
    .commitment-left {
      top: 16%;
    }
    .commitment-right {
      top: 16%;
      left: 70%;
      width: 27%;
    }
    .commitment-title {
      top: 39%;
      left: 24%;
      width: 52%;
      font-size: 76px;
      line-height: 1.02;
    }
    .commitment-center {
      top: 63%;
      left: 37%;
      width: 31%;
      font-size: 31px;
      line-height: 1.2;
    }
    .thanks {
      left: 10%;
      width: 80%;
      top: 36%;
      font-size: 165px;
    }
    .mobile-hint {
      display: block;
      position: absolute;
      right: 4%;
      bottom: 5%;
      color: #5f16e6;
      font-size: 44px;
      font-weight: 700;
      letter-spacing: 0.01em;
      opacity: 0.9;
      background: rgba(255, 255, 255, 0.8);
      padding: 0.2em 0.35em;
      border-radius: 0.3em;
    }
  }
---

<img class="logo-left" src="assets/laravel-community-vadodara/logo-user-groups.png" alt="User Groups logo" />
<img class="hero-community-connect" src="assets/laravel-community-vadodara/logo-community-connect-hero.png" alt="Community Connect" />
<p class="mobile-hint">Swipe to navigate</p>

---

<img class="logo-left" src="assets/laravel-community-vadodara/logo-user-groups.png" alt="User Groups logo" />
<img class="logo-right" src="assets/laravel-community-vadodara/logo-community-connect-small.png" alt="Community Connect logo" />

<img class="panel-black" src="assets/laravel-community-vadodara/panel-black-large.png" alt="" />
<img class="panel-purple-left" src="assets/laravel-community-vadodara/panel-purple-left.png" alt="" />
<img class="logo-laravel" src="assets/laravel-community-vadodara/logo-laravel.png" alt="Laravel logo" />

<h1 class="intro-title">Laravel Community Vadodara</h1>
<p class="intro-subtitle">We are not the largest community.<br />But we are intentional about who we gather and why we gather.</p>

<img class="footer-pill" src="assets/laravel-community-vadodara/footer-pill-yellow.png" alt="" />
<img class="footer-dot" src="assets/laravel-community-vadodara/footer-dot-black.png" alt="" />
<p class="footer-date">1st march</p>

---

<img class="logo-left" src="assets/laravel-community-vadodara/logo-user-groups.png" alt="User Groups logo" />
<img class="logo-right" src="assets/laravel-community-vadodara/logo-community-connect-small.png" alt="Community Connect logo" />
<img class="panel-purple-large" src="assets/laravel-community-vadodara/panel-purple-large.png" alt="" />

<h2 class="content-title">What We're Proud Of</h2>
<ul class="content-list">
  <li>A consistent group of 30-40 professional developers</li>
  <li>Strong foundation in PHP and backend engineering</li>
  <li>Serious learners who value technical depth</li>
  <li>Focused participation over casual attendance</li>
</ul>

<img class="footer-pill" src="assets/laravel-community-vadodara/footer-pill-yellow.png" alt="" />
<img class="footer-dot" src="assets/laravel-community-vadodara/footer-dot-black.png" alt="" />
<p class="footer-date">1st march</p>

---

<img class="logo-left" src="assets/laravel-community-vadodara/logo-user-groups.png" alt="User Groups logo" />
<img class="logo-right" src="assets/laravel-community-vadodara/logo-community-connect-small.png" alt="Community Connect logo" />
<img class="panel-purple-large" src="assets/laravel-community-vadodara/panel-purple-large.png" alt="" />

<h2 class="content-title">What We Aim to Build</h2>
<ul class="content-list">
  <li>Properly curated technical sessions</li>
  <li>Clear topic-focused meetups</li>
  <li>Speaker-audience alignment</li>
  <li>Sessions where attendees know exactly what they will learn</li>
</ul>

<img class="footer-pill" src="assets/laravel-community-vadodara/footer-pill-yellow.png" alt="" />
<img class="footer-dot" src="assets/laravel-community-vadodara/footer-dot-black.png" alt="" />
<p class="footer-date">1st march</p>

---

<img class="logo-left" src="assets/laravel-community-vadodara/logo-user-groups.png" alt="User Groups logo" />
<img class="logo-right" src="assets/laravel-community-vadodara/logo-community-connect-small.png" alt="Community Connect logo" />
<img class="panel-purple-large" src="assets/laravel-community-vadodara/panel-purple-large.png" alt="" />

<h2 class="content-title">What We Give to the Ecosystem</h2>
<ul class="content-list content-list--tight">
  <li>A technically serious audience</li>
  <li>Curated subject-matter focused sessions</li>
  <li>Quality over quantity events</li>
  <li>A space for deep discussions and real problem-solving</li>
  <li>Collaboration-ready mindset</li>
</ul>

<img class="footer-pill" src="assets/laravel-community-vadodara/footer-pill-yellow.png" alt="" />
<img class="footer-dot" src="assets/laravel-community-vadodara/footer-dot-black.png" alt="" />
<p class="footer-date">1st march</p>

---

<img class="logo-left" src="assets/laravel-community-vadodara/logo-user-groups.png" alt="User Groups logo" />
<img class="logo-right" src="assets/laravel-community-vadodara/logo-community-connect-small.png" alt="Community Connect logo" />
<img class="panel-purple-large" src="assets/laravel-community-vadodara/panel-purple-large.png" alt="" />

<h2 class="content-title">What We Need</h2>
<ul class="content-list">
  <li>Consistency in hosting meaningful sessions</li>
  <li>Subject-matter experts willing to go deep</li>
</ul>

<img class="footer-pill" src="assets/laravel-community-vadodara/footer-pill-yellow.png" alt="" />
<img class="footer-dot" src="assets/laravel-community-vadodara/footer-dot-black.png" alt="" />
<p class="footer-date">1st march</p>

---

<img class="logo-left" src="assets/laravel-community-vadodara/logo-user-groups.png" alt="User Groups logo" />
<img class="logo-right" src="assets/laravel-community-vadodara/logo-community-connect-small.png" alt="Community Connect logo" />
<img class="panel-purple-large" src="assets/laravel-community-vadodara/panel-purple-large.png" alt="" />

<p class="commitment-left">Clarity.<br />Depth.<br />Intentional growth.</p>
<p class="commitment-right">If we collaborate -<br />it will be purposeful.</p>
<h2 class="commitment-title">Our Commitment</h2>
<p class="commitment-center">If we host something -<br />it will be meaningful.</p>

<img class="footer-pill" src="assets/laravel-community-vadodara/footer-pill-yellow.png" alt="" />
<img class="footer-dot" src="assets/laravel-community-vadodara/footer-dot-black.png" alt="" />
<p class="footer-date">1st march</p>

---

<img class="logo-left" src="assets/laravel-community-vadodara/logo-user-groups.png" alt="User Groups logo" />
<img class="logo-right" src="assets/laravel-community-vadodara/logo-community-connect-small.png" alt="Community Connect logo" />
<h1 class="thanks">Thank You!</h1>
