# Everyday AI Shopify Theme - Student Tutorial

A complete guide for students to build a custom Shopify theme from scratch, transforming a standard theme into a branded experience for the Everyday AI merch store.

## 🎯 Learning Objectives

By completing this tutorial, students will learn:

- **Shopify theme development** fundamentals and best practices
- **Liquid templating** language for dynamic content
- **CSS customization** with custom properties and responsive design
- **Git workflow** with atomic commits for theme development
- **Brand integration** from existing website to e-commerce platform
- **Theme deployment** and preview management

## 📋 Prerequisites

Before starting, ensure you have:

1. **Shopify Partner Account** (free at [partners.shopify.com](https://partners.shopify.com))
2. **Shopify CLI installed** 
3. **Git installed** and configured
4. **Code editor** (VS Code recommended)
5. **Development store** created in your Shopify Partner dashboard

### Quick Setup Check
```bash
# Verify installations
shopify version
git --version
```

## 🚀 Complete Tutorial: Building the Everyday AI Theme

## Step 1: Initialize Your Shopify Theme Project

### 1.1 Create Development Store
1. Log into [Shopify Partners](https://partners.shopify.com)
2. Go to **Stores** → **Add store** → **Development store**
3. Choose **Create store to test and build**
4. Store name: `your-name-ai-store`
5. Save the store URL (e.g., `your-name-ai-store.myshopify.com`)

### 1.2 Set Up Local Development Environment
```bash
# Create project directory
mkdir shopify_theme_tutorial
cd shopify_theme_tutorial

# Initialize a new Shopify theme (choose Dawn theme as base)
shopify theme init --clone-url https://github.com/Shopify/dawn.git

# Navigate into theme directory
cd dawn

# Connect to your development store
shopify theme dev --store your-name-ai-store.myshopify.com
```

### 1.3 Initialize Git Repository
```bash
# Initialize Git
git init

# Create .gitignore for Shopify
echo "config.yml
.env
*.log
.DS_Store
node_modules/
*.zip" > .gitignore

# Make initial commit
git add .
git commit -m "feat: Initialize Dawn theme for Everyday AI customization"

# Connect to remote repository (replace with your GitHub repo)
git remote add origin git@github.com:yourusername/your-repo-name.git
git branch -M main
git push -u origin main
```

## Step 2: Analyze and Create Design System

### 2.1 Study the Original Website
Before customizing, analyze the existing Everyday AI website design:

1. **Color Palette Analysis**
   - Primary: `#1d4035` (Forest Teal)
   - Accent: `#b85a1f` (Burnt Sienna)  
   - Background: `#fefdfb` (Warm White)
   - Sections: `#f7f5f0` (Cream)

2. **Typography System**
   - Clean, modern sans-serif fonts
   - Hierarchical heading structure
   - Professional, trustworthy tone

3. **Layout Patterns**
   - Hero sections with clear CTAs
   - Grid-based content organization
   - Sticky navigation
   - Mobile-first responsive design

### 2.2 Create Style Guide Documentation
```bash
# Create documentation directory
mkdir docs

# Create style guide
cat > docs/style_guide.md << 'EOF'
# Everyday AI Design System

## Brand Identity
- **Aesthetic**: Explorer/Sage - Earthy, natural, grounded
- **Tone**: Professional yet approachable, educational, trustworthy

## Color System
```css
:root {
  --primary: #1d4035;        /* Forest Teal */
  --accent: #b85a1f;         /* Burnt Sienna */
  --background: #fefdfb;     /* Warm White */
  --surface: #f7f5f0;        /* Cream */
}
```

[Add complete style guide content...]
EOF
```

## Step 3: Create Custom Brand Styling

### 3.1 Create Brand CSS File
```bash
# Create custom CSS file with Liquid support
cat > assets/everyday-ai-branding.css.liquid << 'EOF'
/* ============================================
   EVERYDAY AI - SHOPIFY THEME BRANDING
   Design System: Modern, Professional, Trust-Building
   ============================================ */

:root {
    /* Dynamic colors from theme settings */
    --primary: {{ settings.brand_primary | default: '#1d4035' }};
    --accent: {{ settings.brand_accent | default: '#b85a1f' }};
    --background: {{ settings.brand_warm_white | default: '#fefdfb' }};
    --surface: {{ settings.brand_cream | default: '#f7f5f0' }};
    
    /* Typography */
    --font-heading: 'Helvetica Neue', Arial, sans-serif;
    --font-body: 'Helvetica Neue', Arial, sans-serif;
}

/* Button System */
.btn-primary {
    background: var(--accent);
    color: white;
    border: none;
    padding: 12px 24px;
    border-radius: 6px;
    font-weight: 600;
    transition: all 0.3s ease;
}

.btn-primary:hover {
    background: var(--primary);
    transform: translateY(-2px);
}

[Add complete CSS system...]
EOF
```

### 3.2 Update Theme Layout
```bash
# Edit layout/theme.liquid to include custom CSS
# Add before closing </head> tag:
```

Add this line to `layout/theme.liquid`:
```liquid
<link rel="stylesheet" href="{{ 'everyday-ai-branding.css' | asset_url }}">
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css">
```

### 3.3 Commit Styling Changes
```bash
git add assets/everyday-ai-branding.css.liquid layout/theme.liquid
git commit -m "feat: Add Everyday AI brand CSS system with dynamic colors"
```

## Step 4: Build Custom Theme Sections

### 4.1 Create Hero Section
```bash
# Create hero section for homepage
cat > sections/everyday-ai-hero.liquid << 'EOF'
<section class="everyday-ai-hero">
  <div class="hero-container">
    <div class="hero-content">
      <h1 class="hero-title">{{ section.settings.title }}</h1>
      <p class="hero-subtitle">{{ section.settings.subtitle }}</p>
      <p class="hero-description">{{ section.settings.description }}</p>
      
      {% if section.settings.show_cta %}
        <div class="hero-actions">
          <a href="{{ section.settings.cta_link }}" class="btn-primary">
            {{ section.settings.cta_text }}
          </a>
        </div>
      {% endif %}
    </div>
  </div>
</section>

{% schema %}
{
  "name": "Everyday AI Hero",
  "settings": [
    {
      "type": "text",
      "id": "title",
      "label": "Hero Title",
      "default": "Everyday AI"
    },
    {
      "type": "text", 
      "id": "subtitle",
      "label": "Subtitle",
      "default": "WITH KEITH WILLIAMS"
    },
    {
      "type": "textarea",
      "id": "description", 
      "label": "Description",
      "default": "Free Monthly Town Hall • Newark, NJ & Online"
    },
    {
      "type": "checkbox",
      "id": "show_cta",
      "label": "Show Call to Action",
      "default": true
    },
    {
      "type": "text",
      "id": "cta_text",
      "label": "Button Text",
      "default": "Join Our Community"
    },
    {
      "type": "url",
      "id": "cta_link",
      "label": "Button Link"
    }
  ],
  "presets": [
    {
      "name": "Everyday AI Hero"
    }
  ]
}
{% endschema %}
EOF
```

### 4.2 Create About Keith Section
```bash
# Create About Keith section
cat > sections/about-keith.liquid << 'EOF'
<section class="about-keith-section">
  <div class="container">
    <div class="about-keith-grid">
      <div class="keith-profile">
        {% if section.settings.keith_image %}
          <img src="{{ section.settings.keith_image | image_url: width: 400 }}" 
               alt="Keith Williams" class="keith-image">
        {% endif %}
        <div class="keith-bio">
          <h2>{{ section.settings.title }}</h2>
          <div class="keith-description">
            {{ section.settings.description }}
          </div>
        </div>
      </div>
      
      <div class="credentials-grid">
        {% for block in section.blocks %}
          {% case block.type %}
            {% when 'credential' %}
              <div class="credential-item">
                <i class="{{ block.settings.icon }}"></i>
                <h3>{{ block.settings.title }}</h3>
                <p>{{ block.settings.description }}</p>
              </div>
          {% endcase %}
        {% endfor %}
      </div>
    </div>
  </div>
</section>

{% schema %}
{
  "name": "About Keith Williams",
  "settings": [
    {
      "type": "text",
      "id": "title",
      "label": "Section Title",
      "default": "About Keith Williams"
    },
    {
      "type": "image_picker",
      "id": "keith_image",
      "label": "Keith's Photo"
    },
    {
      "type": "richtext",
      "id": "description",
      "label": "Bio Description"
    }
  ],
  "blocks": [
    {
      "type": "credential",
      "name": "Credential",
      "settings": [
        {
          "type": "text",
          "id": "icon",
          "label": "Font Awesome Icon Class",
          "default": "fas fa-graduation-cap"
        },
        {
          "type": "text",
          "id": "title",
          "label": "Credential Title"
        },
        {
          "type": "text",
          "id": "description",
          "label": "Credential Description"
        }
      ]
    }
  ],
  "presets": [
    {
      "name": "About Keith Williams"
    }
  ]
}
{% endschema %}
EOF
```

### 4.3 Create Additional Sections
Continue creating sections for:
- Town Hall Info (`sections/town-hall-info.liquid`)
- Newsletter Signup (`sections/newsletter-signup.liquid`)

### 4.4 Commit Section Changes
```bash
git add sections/
git commit -m "feat: Add custom Everyday AI homepage sections

- Create hero section with schema for customization
- Add About Keith section with credentials grid
- Include Font Awesome icon support
- Implement responsive design patterns"
```

## Step 5: Configure Theme Settings

### 5.1 Add Theme Customization Options
```bash
# Update config/settings_schema.json to add Everyday AI settings
# Add after the theme_info section:
```

```json
{
  "name": "Everyday AI Branding",
  "settings": [
    {
      "type": "header",
      "content": "Brand Identity"
    },
    {
      "type": "text",
      "id": "site_title",
      "label": "Site Title",
      "default": "Everyday AI"
    },
    {
      "type": "text",
      "id": "site_subtitle",
      "label": "Site Subtitle", 
      "default": "WITH KEITH WILLIAMS"
    },
    {
      "type": "textarea",
      "id": "site_tagline",
      "label": "Site Tagline",
      "default": "Free Monthly Town Hall • Newark, NJ & Online"
    },
    {
      "type": "header",
      "content": "Colors - Everyday AI Palette"
    },
    {
      "type": "color",
      "id": "brand_primary",
      "label": "Primary (Forest Teal)",
      "default": "#1d4035"
    },
    {
      "type": "color", 
      "id": "brand_accent",
      "label": "Accent (Burnt Sienna)",
      "default": "#b85a1f"
    },
    {
      "type": "color",
      "id": "brand_warm_white", 
      "label": "Background (Warm White)",
      "default": "#fefdfb"
    },
    {
      "type": "color",
      "id": "brand_cream",
      "label": "Section Background (Cream)",
      "default": "#f7f5f0"
    }
  ]
}
```

### 5.2 Create Navigation Component
```bash
# Create custom navigation snippet
cat > snippets/everyday-ai-nav.liquid << 'EOF'
{% if settings.show_everyday_ai_nav %}
<nav class="everyday-ai-nav">
  <div class="nav-container">
    <div class="nav-brand">
      <a href="{{ routes.root_url }}">
        {% if settings.logo %}
          <img src="{{ settings.logo | image_url: width: 150 }}" alt="{{ shop.name }}">
        {% else %}
          <span class="nav-title">{{ settings.site_title | default: shop.name }}</span>
          <span class="nav-subtitle">{{ settings.site_subtitle }}</span>
        {% endif %}
      </a>
    </div>
    
    <ul class="nav-menu">
      <li><a href="{{ routes.root_url }}">Home</a></li>
      <li><a href="#about-keith">About Keith</a></li>
      <li><a href="#town-hall">Town Hall</a></li>
      <li><a href="{{ routes.collections_url }}">Shop</a></li>
      <li>
        <a href="{{ routes.cart_url }}" class="cart-link">
          <i class="fas fa-shopping-cart"></i>
          <span class="cart-count">{{ cart.item_count }}</span>
        </a>
      </li>
    </ul>
  </div>
</nav>
{% endif %}
EOF
```

### 5.3 Update Homepage Template
```bash
# Create custom homepage template
cat > templates/index.json << 'EOF'
{
  "sections": {
    "everyday-ai-hero": {
      "type": "everyday-ai-hero",
      "settings": {
        "title": "Everyday AI",
        "subtitle": "WITH KEITH WILLIAMS", 
        "description": "Free Monthly Town Hall • Newark, NJ & Online",
        "show_cta": true,
        "cta_text": "Join Our Community",
        "cta_link": "#newsletter-signup"
      }
    },
    "about-keith": {
      "type": "about-keith",
      "blocks": {
        "credential_1": {
          "type": "credential",
          "settings": {
            "icon": "fas fa-university",
            "title": "NJIT Professor",
            "description": "Information Systems & Computer Science"
          }
        },
        "credential_2": {
          "type": "credential", 
          "settings": {
            "icon": "fas fa-briefcase",
            "title": "40+ Years",
            "description": "Technology Leadership Experience"
          }
        },
        "credential_3": {
          "type": "credential",
          "settings": {
            "icon": "fas fa-robot",
            "title": "AI Expert",
            "description": "Practical AI Implementation & Strategy"
          }
        }
      },
      "block_order": ["credential_1", "credential_2", "credential_3"]
    },
    "town-hall-info": {
      "type": "town-hall-info"
    },
    "newsletter-signup": {
      "type": "newsletter-signup"
    }
  },
  "order": [
    "everyday-ai-hero",
    "about-keith", 
    "town-hall-info",
    "newsletter-signup"
  ]
}
EOF
```

## Step 6: Deploy and Test Your Theme

### 6.1 Deploy to Development Store
```bash
# Push theme to your development store
shopify theme push --store your-name-ai-store.myshopify.com --unpublished

# Note the theme ID from the output (e.g., #136569094231)
```

### 6.2 Preview Your Theme
```bash
# Get preview URL (replace THEME_ID with actual ID)
shopify theme info --store your-name-ai-store.myshopify.com --theme THEME_ID

# Or start development mode for live updates
shopify theme dev --store your-name-ai-store.myshopify.com --theme THEME_ID
```

### 6.3 Access Theme Customizer
1. Go to your store admin: `https://your-name-ai-store.myshopify.com/admin`
2. Navigate to **Online Store** → **Themes**
3. Find your theme and click **Customize**
4. Explore the "Everyday AI Branding" settings section

## Step 7: Advanced Customizations (Optional)

### 7.1 Add Footer Component
```bash
# Create branded footer
cat > snippets/everyday-ai-footer.liquid << 'EOF'
<footer class="everyday-ai-footer">
  <div class="footer-container">
    <div class="footer-brand">
      <h3>{{ settings.site_title }}</h3>
      <p>{{ settings.site_tagline }}</p>
    </div>
    <div class="footer-links">
      <h4>Quick Links</h4>
      <ul>
        <li><a href="{{ routes.root_url }}">Home</a></li>
        <li><a href="#about-keith">About Keith</a></li>
        <li><a href="#town-hall">Town Hall</a></li>
        <li><a href="{{ routes.collections_url }}">Shop</a></li>
      </ul>
    </div>
  </div>
</footer>
EOF
```

### 7.2 Create Product Templates
- Customize `templates/product.json` for consistent branding
- Add custom product sections if needed

### 7.3 Mobile Optimization
```css
/* Add to your CSS file */
@media (max-width: 768px) {
  .hero-container {
    padding: 2rem 1rem;
    text-align: center;
  }
  
  .nav-menu {
    display: none; /* Implement hamburger menu */
  }
}
```

## Step 8: Final Deployment and Testing

### 8.1 Complete Git Workflow
```bash
# Add all changes
git add .

# Create comprehensive commit
git commit -m "feat: Complete Everyday AI theme transformation

- Add custom branding with dynamic color system
- Create homepage sections (hero, about Keith, town hall, newsletter)
- Implement responsive navigation with cart integration  
- Add theme customization settings for brand colors
- Include Font Awesome icons and mobile optimization
- Create branded footer with social links
- Update homepage template with structured sections"

# Push to remote repository
git push origin main
```

### 8.2 Theme Testing Checklist
- [ ] **Desktop Navigation**: All menu items work correctly
- [ ] **Mobile Responsiveness**: Theme displays properly on mobile devices
- [ ] **Color Customization**: Theme colors update when changed in settings
- [ ] **Cart Functionality**: Add to cart and cart count work
- [ ] **Form Submissions**: Newsletter signup processes correctly
- [ ] **Image Optimization**: All images load with proper alt text
- [ ] **Performance**: Page loads quickly with optimized CSS/JS

### 8.3 Production Deployment
```bash
# When ready for production
shopify theme publish --store your-name-ai-store.myshopify.com --theme THEME_ID

# Or share with others for review
shopify theme share --store your-name-ai-store.myshopify.com --theme THEME_ID
```

## 📚 Key Learning Concepts

### Shopify Theme Development
- **Liquid Templating**: Dynamic content rendering with variables and logic
- **Section Schema**: Creating customizable theme sections with settings
- **Asset Management**: CSS, JavaScript, and image optimization
- **Theme Structure**: Understanding Shopify's file organization

### CSS & Design Systems
- **Custom Properties**: Using CSS variables for dynamic theming
- **Responsive Design**: Mobile-first development principles
- **Component Architecture**: Modular, reusable styling patterns
- **Brand Consistency**: Maintaining design system across all pages

### Git & Version Control
- **Atomic Commits**: Small, focused commits with clear messages
- **Branch Management**: Using feature branches for development
- **Collaboration**: Working with remote repositories and teams
- **Documentation**: Writing clear README files and code comments

### E-commerce Integration
- **Cart Functionality**: Shopify's cart system and Liquid objects
- **Product Management**: Templates and customization options
- **Customer Experience**: Navigation, forms, and user interactions
- **Performance**: Optimization for fast loading and SEO

## 🎯 Project Outcomes

After completing this tutorial, you will have:

✅ **Professional Shopify Theme** with custom branding and design  
✅ **Development Workflow** using Git, Shopify CLI, and best practices  
✅ **Responsive Website** optimized for all devices and screen sizes  
✅ **Theme Customization** system through Shopify's admin interface  
✅ **Brand Integration** from existing website to e-commerce platform  
✅ **Production-Ready Code** with proper documentation and structure  

## Final File Structure

```
shopify-theme-tutorial/
├── assets/
│   └── everyday-ai-branding.css.liquid    # Dynamic brand styling
├── config/
│   └── settings_schema.json               # Theme customization options  
├── docs/
│   └── style_guide.md                     # Design system documentation
├── layout/
│   └── theme.liquid                       # Main theme layout with nav/footer
├── sections/
│   ├── everyday-ai-hero.liquid           # Homepage hero section
│   ├── about-keith.liquid               # Keith Williams profile
│   ├── town-hall-info.liquid            # AI meetup information
│   └── newsletter-signup.liquid         # Email capture form
├── snippets/
│   ├── everyday-ai-nav.liquid           # Custom navigation component
│   └── everyday-ai-footer.liquid       # Branded footer component
├── templates/
│   ├── index.json                       # Custom homepage template
│   └── page.about-keith.json           # About Keith page template
├── .gitignore                           # Git ignore patterns
└── README.md                            # This comprehensive guide
```

## 🔧 Troubleshooting Common Issues

### Theme Push Errors
```bash
# If you get "Invalid value for block" errors:
# Check that static blocks aren't in block_order arrays

# If theme validation fails:
shopify theme check
```

### CLI Connection Issues
```bash
# Reconnect to store if authentication fails
shopify auth logout
shopify auth login

# Verify store connection
shopify theme list --store your-store-name.myshopify.com
```

### CSS Not Loading
```bash
# Ensure CSS file has .liquid extension for dynamic variables
mv assets/styles.css assets/styles.css.liquid

# Check theme.liquid includes the stylesheet
# <link rel="stylesheet" href="{{ 'everyday-ai-branding.css' | asset_url }}">
```

### Git Repository Issues
```bash
# If remote repository doesn't exist, create it first on GitHub
# Then connect:
git remote add origin git@github.com:username/repository-name.git
git push -u origin main
```

## 💡 Advanced Challenges (For Advanced Students)

### Challenge 1: Add Blog Integration
- Create custom blog template with Everyday AI branding
- Add author bio sections for Keith Williams posts
- Implement related posts functionality

### Challenge 2: Implement Search Functionality  
- Create custom search page with branded styling
- Add search filters for product categories
- Implement autocomplete search suggestions

### Challenge 3: Add Customer Account Pages
- Customize login/register pages with brand colors
- Create customer dashboard with order history
- Add wishlist functionality for products

### Challenge 4: Performance Optimization
- Implement lazy loading for images
- Optimize CSS/JS bundle sizes
- Add service worker for offline functionality

## 📖 Additional Resources

### Official Documentation
- [Shopify Theme Development](https://shopify.dev/themes)
- [Liquid Template Language](https://shopify.github.io/liquid/)
- [Shopify CLI Reference](https://shopify.dev/themes/tools/cli)

### Learning Resources
- [Shopify Partner Academy](https://academy.shopify.com)
- [Theme Inspector Chrome Extension](https://chrome.google.com/webstore/detail/shopify-theme-inspector/fndnankcflemoafdeboboehphmiijkgp)
- [Liquid Cheat Sheet](https://www.shopify.com/partners/shopify-cheat-sheet)

### Community & Support
- [Shopify Community Forums](https://community.shopify.com)
- [GitHub Shopify Themes](https://github.com/Shopify/dawn)
- [Shopify Partners Slack](https://shopifypartners.slack.com)

## 🎓 Assignment Deliverables

### Required Submissions
1. **GitHub Repository URL** with complete theme code
2. **Live Preview URL** of your deployed theme
3. **Screenshot Portfolio** showing:
   - Homepage (desktop and mobile)
   - Navigation functionality
   - Theme customizer with your brand colors
   - At least one product page
4. **Reflection Document** (500 words) covering:
   - Technical challenges encountered and solutions
   - Design decisions and brand integration process
   - Learning outcomes and skill development
   - Ideas for future improvements

### Grading Criteria
- **Code Quality (30%)**: Clean, well-commented code with proper Git workflow
- **Design Implementation (25%)**: Faithful recreation of brand identity and responsive design
- **Functionality (20%)**: All features working correctly (navigation, cart, forms)
- **Customization (15%)**: Proper theme settings and admin integration
- **Documentation (10%)**: Clear README and code comments

### Due Date Extensions
Students may request a 48-hour extension by demonstrating:
- Significant progress on core functionality
- Documented technical blockers with attempted solutions
- Clear plan for completion within extension period

## 👥 Collaboration Guidelines

### Pair Programming (Optional)
Students may work in pairs with these requirements:
- Both students must contribute to all aspects of the project
- Git commits must clearly identify individual contributions
- Each student submits their own reflection document
- Both students must be able to explain all code during presentation

### Code Review Process
1. **Peer Review**: Exchange repositories with classmates for feedback
2. **Instructor Review**: Schedule 15-minute code review sessions
3. **Documentation**: Document feedback received and implemented changes

## 🏆 Bonus Opportunities (+10 points each)

### Advanced Features
- **Accessibility Compliance**: Implement WCAG 2.1 AA standards
- **Internationalization**: Add multi-language support with Shopify's system
- **Performance Optimization**: Achieve 90+ Google Lighthouse score
- **Advanced Animations**: CSS/JS animations that enhance user experience
- **Custom Apps**: Integration with Shopify apps for extended functionality

### Community Contribution
- **Open Source**: Make theme available as open-source template
- **Tutorial Blog Post**: Write detailed blog post about your development process
- **Video Walkthrough**: Create screencast tutorial for other students
- **Stack Overflow**: Answer Shopify development questions with theme examples

## 📝 Final Reflection Questions

Consider these questions in your reflection document:

1. **Technical Growth**: What Shopify/Liquid concepts were most challenging to grasp?
2. **Design Process**: How did you approach translating a static design to dynamic theme?
3. **Problem Solving**: Describe your debugging process when encountering errors.
4. **User Experience**: What considerations did you make for different user types?
5. **Future Development**: How would you extend this theme for a real client?
6. **Industry Relevance**: How do these skills apply to modern web development?

## 🎯 Success Metrics

By project completion, successful students will demonstrate:

✅ **Proficiency in Liquid templating** with dynamic content and logic  
✅ **Understanding of Shopify theme architecture** and file organization  
✅ **CSS skills with modern techniques** including custom properties and responsive design  
✅ **Git workflow competency** with meaningful commits and documentation  
✅ **Brand translation abilities** from static design to dynamic e-commerce platform  
✅ **Problem-solving skills** through debugging and optimization processes  
✅ **Professional development practices** with code organization and documentation  

---

## 🌟 Instructor Notes

### Setup Requirements
- Ensure all students have Shopify Partner accounts before class
- Provide development store creation walkthrough
- Verify CLI installations work across different operating systems
- Have backup theme files ready for students with technical difficulties

### Common Teaching Points
- Emphasize atomic commits and meaningful commit messages
- Demonstrate debugging techniques for Liquid template errors
- Show theme inspector browser extension usage
- Explain the difference between static and dynamic blocks
- Review responsive design testing across multiple devices

### Assessment Rubric Available
Detailed rubric available in course management system with specific criteria for:
- Code organization and commenting standards
- Design implementation accuracy and creativity
- Technical functionality and error handling
- Git workflow and collaboration practices
- Documentation quality and completeness

---

**Built for Student Success**  
*Preparing the next generation of Shopify developers*