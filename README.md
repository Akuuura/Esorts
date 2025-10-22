# Everyday AI Shopify Theme

A custom Shopify theme designed for the Everyday AI merch store, featuring Keith Williams and the AI town hall community.

## Overview

This theme transforms a standard Shopify store into a branded experience for the Everyday AI community, featuring:

- **Professional branding** with earthy, trust-building color scheme
- **Responsive design** optimized for all devices 
- **Custom homepage** showcasing Keith Williams and the AI town hall
- **Integrated navigation** with smooth scrolling and mobile support
- **Theme customization** through Shopify's admin interface

## Design System

### Color Palette
- **Primary (Forest Teal)**: `#1d4035` - Main brand color for headers, navigation
- **Accent (Burnt Sienna)**: `#b85a1f` - Call-to-action buttons, highlights  
- **Warm White**: `#fefdfb` - Main background color
- **Cream**: `#f7f5f0` - Section backgrounds and cards

### Typography
- Clean, modern sans-serif fonts
- Hierarchical heading system (H1-H6)
- Readable body text with proper line height
- Responsive font scaling

## Key Features

### Homepage Sections
1. **Hero Section** - Introduction to Keith Williams and Everyday AI
2. **About Keith** - Credentials and professional background
3. **Town Hall Info** - Information about monthly AI meetups
4. **Newsletter Signup** - Email capture for community updates
5. **Merch Preview** - Featured products showcase

### Navigation
- Sticky header with brand logo/text
- Main menu: Home, About Keith, Town Hall, Shop
- Shopping cart indicator with item count
- Mobile-responsive hamburger menu

### Footer
- Contact information and quick links
- Social media integration (Twitter, LinkedIn, YouTube)
- Policy links and shop information
- Copyright and community branding

## Theme Settings

Access **Customize Theme** in Shopify admin to configure:

### Everyday AI Branding
- Site title and subtitle
- Site tagline for town hall info
- Navigation toggle and custom links
- Brand color customization

### Social Media
- Twitter URL
- LinkedIn URL  
- YouTube URL

### Logo & Favicon
- Upload custom logo
- Set favicon for browser tabs

## File Structure

```
/
├── assets/
│   └── everyday-ai-branding.css.liquid    # Main brand styling
├── config/
│   └── settings_schema.json               # Theme customization options
├── docs/
│   ├── guide/theme.md                     # Development guide
│   └── style_guide.md                     # Design system documentation
├── layout/
│   └── theme.liquid                       # Main theme layout
├── sections/
│   ├── everyday-ai-hero.liquid           # Homepage hero section
│   ├── about-keith.liquid               # Keith Williams profile
│   ├── town-hall-info.liquid            # AI meetup information
│   └── newsletter-signup.liquid         # Email capture form
├── snippets/
│   ├── everyday-ai-nav.liquid           # Main navigation
│   └── everyday-ai-footer.liquid       # Site footer
└── templates/
    └── index.json                       # Homepage template
```

## Development

### Prerequisites
- Shopify CLI installed
- Shopify Partner account
- Git repository access

### Local Development

1. **Clone the repository**
   ```bash
   git clone git@github.com:kaw393939/shopify_theme_373.git
   cd shopify_theme_373
   ```

2. **Connect to Shopify store**
   ```bash
   shopify theme dev --store your-store-name
   ```

3. **Make changes**
   - Edit Liquid templates in `sections/`, `snippets/`, `templates/`
   - Modify styling in `assets/everyday-ai-branding.css.liquid`
   - Update settings in `config/settings_schema.json`

4. **Deploy changes**
   ```bash
   shopify theme push --theme your-theme-id
   ```

### Customization Guide

#### Adding New Sections
1. Create new `.liquid` file in `sections/` directory
2. Include schema for theme editor settings
3. Add to homepage via `templates/index.json`

#### Modifying Colors
1. Update CSS custom properties in `assets/everyday-ai-branding.css.liquid`
2. Or use theme customizer in Shopify admin

#### Adding Content
1. Use theme sections through Shopify admin
2. Edit Liquid templates for hardcoded content
3. Configure settings through theme customizer

## Brand Guidelines

### Voice & Tone
- **Professional yet approachable**
- **Educational and empowering**
- **Community-focused**
- **Technology-forward but accessible**

### Visual Identity
- Clean, modern layouts with plenty of white space
- Professional photography and imagery
- Consistent use of brand colors and typography
- Mobile-first responsive design

### Content Strategy
- Focus on AI education and community building
- Showcase Keith Williams' expertise and credentials
- Promote monthly town hall events
- Encourage community engagement and learning

## Browser Support

- **Chrome** (latest 2 versions)
- **Firefox** (latest 2 versions)  
- **Safari** (latest 2 versions)
- **Edge** (latest 2 versions)
- **Mobile browsers** (iOS Safari, Chrome Mobile)

## Performance

The theme is optimized for:
- Fast loading times with minimal JavaScript
- Efficient CSS with custom properties
- Optimized images and media
- Mobile performance

## Support

For theme support and customization:

1. **Documentation**: Check `docs/` directory for guides
2. **Code Issues**: Create GitHub issues in the repository
3. **Shopify Support**: Use Shopify Partner dashboard for platform issues

## License

Custom theme for Everyday AI community. All rights reserved.

---

**Built for the Everyday AI Community**  
*Empowering everyone with AI knowledge and tools*