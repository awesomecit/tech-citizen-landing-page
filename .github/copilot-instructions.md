# Tech Citizen Landing Page - AI Agent Instructions

## Project Architecture

This is a **build-free** landing page using modern web standards:
- **Stack**: HTML5 + LitElement Web Components + Tailwind CSS + Vanilla JS
- **No build tools**: Direct ES6 modules via CDN (Skypack for LitElement)
- **Component Architecture**: SOLID principles with inheritance hierarchy
- **Methodology**: Extreme Programming (XP) with Test-Driven Development

## Key Architectural Patterns

### Component Hierarchy
```javascript
BaseSection (abstract)
├── HeroSection
├── ServicesSection  
├── ProjectsSection
├── AboutSection
└── ContactForm
```

All components extend `BaseSection` which provides:
- Common i18n integration via `t()` function
- Analytics tracking via `trackEvent()`
- Consistent CSS structure and responsive patterns

### File Organization
```
/
├── index.html (single entry point)
├── js/
│   ├── main.js (app bootstrap)
│   ├── components/ (LitElement components)
│   ├── i18n/locales/ (translation JSON files)
│   ├── data/ (static data models)
│   └── utils/ (services like analytics)
├── css/custom.css (Tailwind extensions)
└── assets/ (images, icons)
```

## Development Workflow

### XP/TDD Approach
1. **Red**: Write failing test first
2. **Green**: Implement minimal code to pass
3. **Refactor**: Improve while keeping tests green

### Component Development Pattern
```javascript
// 1. Extend BaseSection for consistent structure
export class NewSection extends BaseSection {
  static styles = [super.styles, css`/* custom styles */`];
  
  // 2. Override renderContent() method
  renderContent() {
    return html`<!-- component template -->`;
  }
  
  // 3. Add event handlers with analytics
  handleAction() {
    this.trackEvent('action_name', { context: 'data' });
  }
}
```

## Critical Implementation Details

### Internationalization
- Use `t('SECTION.KEY')` for all user-facing text
- Keys stored in `js/i18n/locales/it.json` (dot notation)
- Service handles interpolation: `t('KEY', { param: 'value' })`

### Analytics Integration
- Every user interaction MUST call `this.trackEvent(eventName, data)`
- Automatic tracking: page views, scroll depth, time on page
- Events stored locally, sent to API in production

### Responsive Design Strategy
- Mobile-first Tailwind classes
- Breakpoints: sm(640px), md(768px), lg(1024px)
- Custom CSS for complex responsive behaviors
- Swiper.js for carousels with responsive breakpoints

### Data Loading Patterns
```javascript
// Services/Projects: Handle empty, loading, error states
renderContent() {
  if (this.loading) return this.renderLoadingState();
  if (this.isEmpty) return this.renderEmptyState();
  return this.renderData();
}
```

## Key Development Commands

### Testing & Validation
```bash
# Manual testing (no test framework yet)
# 1. Open index.html in browser
# 2. Check console for errors
# 3. Test responsive breakpoints
# 4. Verify analytics events
```

### Component Registration
```javascript
// Always define custom elements at component end
customElements.define('component-name', ComponentClass);
```

## Production Considerations

### Performance Optimizations
- Service Worker caching for static assets
- Preload critical resources (Tailwind, LitElement CDN)
- WebP image detection and optimization
- Bundle size monitoring (keep minimal)

### SEO Requirements
- Structured data (JSON-LD) for business information
- Open Graph tags for social sharing
- Italian language meta tags and content
- Mobile-first responsive design

## Common Pitfalls to Avoid

1. **CDN Dependencies**: Always use Skypack for ES modules, not npm
2. **Component Lifecycle**: Don't forget `customElements.define()`
3. **i18n Keys**: Use dot notation consistently (`SECTION.SUBSECTION.KEY`)
4. **Analytics**: Track ALL user interactions, not just clicks
5. **Responsive**: Test on mobile breakpoints, not just desktop

## Sprint-Based Development

Project follows 4-week sprint structure:
- **Sprint 1**: Foundation (HTML, i18n, BaseComponent)
- **Sprint 2**: Content sections (Hero, Services, Projects, About, Contact)  
- **Sprint 3**: Interactive features (Carousel, Analytics, Animations)
- **Sprint 4**: Production (SEO, Performance, Deployment)

When implementing features, follow the detailed task breakdowns in `ROADMAP.md` - each task has specific deliverables and acceptance criteria.