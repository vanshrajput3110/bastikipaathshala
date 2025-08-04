

# Basti Ki Pathshala - NGO Website Template

This is a modern, responsive, and highly animated single-page website template designed for an educational non-governmental organization (NGO). The project showcases a clean user interface and engaging user experience through advanced JavaScript animations and a thoughtful, mobile-first design.

## ✨ Features

  * **Single-Page Application (SPA) Feel:** Navigate between Home, About Us, and Volunteer sections seamlessly without page reloads.
  * **Advanced Animations:**
      * **GSAP & ScrollTrigger:** Elements animate into view on scroll, creating a dynamic and engaging experience.
      * **Smooth Page Transitions:** Sections fade in and out gracefully when navigating.
      * **Interactive Elements:** Features "magnetic" buttons that attract the cursor, animated counters, and subtle hover effects on cards.
      * **Background Effects:** Includes an animated gradient background that changes with navigation and parallax background elements.
  * **Fully Responsive Design:** A mobile-first approach ensures the website looks and functions beautifully on all devices, from small phones to large desktops.
  * **Interactive Volunteer Form:** A multi-field application form with client-side validation, a loading state on submission, and an animated success message.
  * **Enhanced UX/UI:**
      * A fixed header that hides on scroll-down and reappears on scroll-up.
      * A side-dot scroll indicator that shows the current section.
      * A "Back" button to easily return to previously viewed sections.
      * Mobile swipe navigation to move between sections.
  * **Modern Tech Stack:** Built with standard web technologies and popular libraries, making it easy to understand and customize.

-----

## 🛠️ Technologies Used

  * **HTML5:** For the core structure and content.
  * **CSS3:** For custom styling, animations, and responsive design (using CSS Variables for a consistent color palette).
  * **Tailwind CSS:** A utility-first CSS framework used for rapid UI development.
  * **JavaScript (ES6+):** For all interactivity, DOM manipulation, and application logic.
  * **GSAP (GreenSock Animation Platform):** A professional-grade JavaScript animation library for high-performance animations.
      * **ScrollTrigger Plugin:** For creating scroll-based animations.
  * **Font Awesome:** For scalable vector icons.

-----

## 🚀 How to Run

This project is self-contained and uses CDN links for all external libraries. No installation or build process is needed.

1.  Clone this repository or download the `index.html` file.
2.  Open the `index.html` file directly in any modern web browser (like Chrome, Firefox, or Edge).

-----

## 📁 File Structure

The entire project is consolidated into a single `index.html` file for simplicity.

  * **`<head>`:** Contains page metadata, CDN links for all dependencies (Tailwind, GSAP, Font Awesome), and all custom CSS within `<style>` tags.
  * **`<body>`:** Holds the HTML for the header, main content sections (`#home`, `#about`, `#volunteer`), and the footer.
  * **`<script>` tag at the end of `<body>`:** Contains all the JavaScript logic for:
      * Navigation and section management.
      * GSAP animations.
      * Event listeners (clicks, scroll, touch).
      * Volunteer form handling.

-----

## 🧠 Code Highlights

### 1\. SPA Navigation Logic

The single-page feel is managed by a `showSection` function. It hides all other sections and displays the target one with a smooth GSAP animation. A `navigationHistory` array tracks the user's path, enabling the "Back" button functionality.

```javascript
let navigationHistory = ['home'];

function showSection(sectionId) {
    // Hide current section
    gsap.to(`#${currentSection}`, {
        opacity: 0,
        duration: 0.5,
        onComplete: () => {
            // Show new section after hiding the old one
            document.getElementById(currentSection).classList.add('hidden');
            showNewSection(sectionId);
        }
    });
}

function goBack(currentSection) {
    navigationHistory.pop();
    const previousSection = navigationHistory[navigationHistory.length - 1] || 'home';
    showSection(previousSection);
}
```

### 2\. Scroll-Based Animations with ScrollTrigger

The `ScrollTrigger` plugin is used to trigger animations as elements enter the viewport. This is used for the "reveal" effect on text, the counting-up animation for statistics, and the floating effect on cards.

```javascript
function setupScrollAnimations() {
    // Animate text reveal elements
    gsap.utils.toArray('.text-reveal').forEach(element => {
        gsap.fromTo(element,
            { opacity: 0, y: 30 },
            {
                opacity: 1, y: 0, duration: 1.2,
                scrollTrigger: {
                    trigger: element,
                    start: 'top 85%', // Animation starts when the top of the element is 85% from the top of the viewport
                    toggleActions: 'play none none reverse'
                }
            }
        );
    });

    // Animate counter numbers
    gsap.utils.toArray('.counter').forEach(counter => {
        // ... GSAP animation logic with a ScrollTrigger
    });
}
```

### 3\. Interactive Volunteer Form

The form submission is handled by the `submitVolunteerForm` function, which prevents the default form submission, shows a loading state, and then displays an animated success message.

```javascript
function submitVolunteerForm(event) {
    event.preventDefault();

    // Simulate form processing and show a loading state
    setTimeout(() => {
        // Fade out the form
        gsap.to('#volunteerForm', {
            opacity: 0,
            y: -30,
            duration: 0.5,
            onComplete: () => {
                // Hide form and show success message
                document.getElementById('volunteerForm').style.display = 'none';
                document.getElementById('successMessage').classList.add('active');

                // Animate success message in
                gsap.fromTo('#successMessage',
                    { opacity: 0, scale: 0.9 },
                    { opacity: 1, scale: 1, duration: 0.6, ease: 'back.out(1.7)' }
                );
            }
        });
    }, 1500); // 1.5-second delay
}
```
