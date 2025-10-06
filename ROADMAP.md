# 🚀 Tech Citizen Landing Page - Project Roadmap

## 📋 Project Overview

**Project**: Landing Page per Consulenza Software Enterprise  
**Domain**: tech-citizen.me  
**Target**: CTO, Tech Lead, HR Manager italiani  
**Stack**: HTML5 + LitElement + Tailwind CSS + Vanilla JS  
**Methodology**: Extreme Programming (XP) + SOLID Principles  
**Delivery**: Incremental releases with continuous testing  

### 🎯 Business Goals

1. **Primary**: Generate qualified enterprise leads
2. **Secondary**: Establish technical credibility  
3. **Tertiary**: Showcase Agile transformation expertise

---

## 🏗️ Architecture & Design Principles

### SOLID Principles Application

#### **S - Single Responsibility Principle**

```javascript
// ✅ Each component has one responsibility
class HeroSection extends LitElement { /* Only hero content */ }
class ProjectsSection extends LitElement { /* Only projects display */ }
class I18nService { /* Only translations */ }
```

#### **O - Open/Closed Principle**

```javascript
// ✅ Extendable without modifying existing code
class BaseSection extends LitElement {
  // Base functionality
}
class ProjectsSection extends BaseSection {
  // Extends base without modification
}
```

#### **L - Liskov Substitution Principle**

```javascript
// ✅ Components are interchangeable
interface SectionComponent {
  render(): TemplateResult;
}
// All sections implement same interface
```

#### **I - Interface Segregation**

```javascript
// ✅ Small, focused interfaces
interface Translatable { t(key: string): string; }
interface Trackable { track(event: string, data: object): void; }
interface Loadable { load(): Promise<void>; }
```

#### **D - Dependency Inversion**

```javascript
// ✅ Depend on abstractions, not concretions
class ProjectsSection {
  constructor(private dataService: ProjectDataService) {}
  // Injected dependency, not hardcoded
}
```

### XP Practices Applied

- **TDD**: Test-first development for each component
- **Refactoring**: Continuous code improvement  
- **Simple Design**: YAGNI - implement only what's needed
- **Pair Programming**: Code review for each task
- **Continuous Integration**: Auto-deploy on main branch

---

## 📖 Epic Stories

### Epic 1: Foundation & Infrastructure

**Value**: Stable, performant base for all features  
**Estimation**: 21 story points  

### Epic 2: Content Sections  

**Value**: Core business content visible to users  
**Estimation**: 34 story points  

### Epic 3: Interactive Features

**Value**: Enhanced UX with dynamic content  
**Estimation**: 21 story points  

### Epic 4: Production & Optimization

**Value**: Live, optimized, monitored solution  
**Estimation**: 13 story points  

**Total**: 89 story points (~3 weeks @ 30 SP/week)

---

## 🎯 Sprint 1: Foundation (Week 1) - 21 SP

### User Story 1.1: Static HTML Structure

**As a** developer  
**I want** a semantic HTML foundation  
**So that** I can build upon solid accessibility and SEO base  

**Acceptance Criteria**:

- [x] Valid HTML5 structure
- [x] Semantic elements (header, main, section, footer)
- [x] Meta tags for SEO
- [x] Mobile viewport configuration

#### Task 1.1.1: Create base HTML structure (2 SP)

```html
<!-- DELIVERABLE: index.html -->
<!DOCTYPE html>
<html lang="it">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Tech Citizen - Consulenza Software Enterprise</title>
  <meta name="description" content="Fractional CTO, Agile Transformation, Formazione Enterprise">
</head>
<body>
  <main id="app"></main>
</body>
</html>
```

#### Task 1.1.2: Setup CSS framework (1 SP)

```html
<!-- DELIVERABLE: Tailwind CSS integration -->
<link href="https://cdn.tailwindcss.com" rel="stylesheet">
<link href="./css/custom.css" rel="stylesheet">
```

#### Task 1.1.3: Configure build-free structure (1 SP)

```
<!-- DELIVERABLE: File structure -->
/
├── index.html
├── css/custom.css  
├── js/main.js
└── assets/
```

**Definition of Done**: HTML validates, loads correctly, responsive meta tags present

---

### User Story 1.2: Internationalization System

**As a** developer  
**I want** a flexible i18n system  
**So that** content is maintainable and extensible  

#### Task 1.2.1: Create i18n base service (3 SP)

```javascript
// DELIVERABLE: js/i18n/i18n.js
class I18nService {
  constructor() {
    this.locale = 'it';
    this.translations = {};
  }
  
  async loadTranslations() {
    const response = await fetch(`./js/i18n/locales/${this.locale}.json`);
    this.translations = await response.json();
  }
  
  t(key, params = {}) {
    const keys = key.split('.');
    let value = this.translations;
    
    for (const k of keys) {
      value = value?.[k];
    }
    
    return value ? this.interpolate(value, params) : key;
  }
  
  interpolate(template, params) {
    return template.replace(/\{\{(\w+)\}\}/g, (match, key) => {
      return params[key] || match;
    });
  }
}

export const t = (key, params) => new I18nService().t(key, params);
```

#### Task 1.2.2: Create Italian translations file (2 SP)

```json
// DELIVERABLE: js/i18n/locales/it.json
{
  "HERO": {
    "TITLE": "Trasformazione Agile Enterprise",
    "SUBTITLE": "con Intelligenza Emotiva",
    "DESCRIPTION": "Fractional CTO • Formazione • Agile",
    "CTA_BUTTON": "Richiedi Consulenza Strategica"
  },
  "SERVICES": {
    "TITLE": "I Nostri Servizi",
    "SOFTWARE_DEV": {
      "TITLE": "Sviluppo Software",
      "DESCRIPTION": "Architetture moderne e scalabili"
    }
  }
}
```

**Definition of Done**: i18n service loads translations, t() function works, fallback to key if missing

---

### User Story 1.3: LitElement Base Components

**As a** developer  
**I want** reusable web components  
**So that** UI is modular and maintainable  

#### Task 1.3.1: Setup LitElement infrastructure (2 SP)

```html
<!-- DELIVERABLE: LitElement CDN integration -->
<script type="importmap">
{
  "imports": {
    "lit": "https://cdn.skypack.dev/lit@2"
  }
}
</script>
```

#### Task 1.3.2: Create base component class (3 SP)

```javascript
// DELIVERABLE: js/components/base-section.js
import { LitElement, html, css } from 'lit';
import { t } from '../i18n/i18n.js';

export class BaseSection extends LitElement {
  static styles = css`
    :host {
      display: block;
    }
  `;
  
  // Common functionality for all sections
  trackEvent(eventName, data = {}) {
    console.log('Track:', eventName, data);
    // Analytics integration point
  }
  
  // Template method pattern
  render() {
    return html`
      <section class="py-16">
        <div class="container mx-auto px-4">
          ${this.renderContent()}
        </div>
      </section>
    `;
  }
  
  // Override in child classes
  renderContent() {
    return html`<p>Base section</p>`;
  }
}
```

#### Task 1.3.3: Create main app component (2 SP)

```javascript
// DELIVERABLE: js/main.js
import { LitElement, html } from 'lit';
import './components/hero-section.js';

class TechCitizenApp extends LitElement {
  render() {
    return html`
      <header><!-- Navigation --></header>
      <main>
        <hero-section></hero-section>
      </main>
      <footer><!-- Footer --></footer>
    `;
  }
}

customElements.define('tech-citizen-app', TechCitizenApp);
```

**Definition of Done**: LitElement components load, render correctly, i18n integration works

---

### User Story 1.4: DNS & Hosting Verification

**As a** user  
**I want** the site accessible via tech-citizen.me  
**So that** I can view the landing page  

#### Task 1.4.1: DNS propagation test (1 SP)

```bash
# DELIVERABLE: Updated DNS test script
#!/bin/bash
DOMAIN="tech-citizen.me"

echo "🌐 Testing DNS for: $DOMAIN"
for dns in "8.8.8.8" "1.1.1.1" "208.67.222.222"; do
    echo -n "  $dns: "
    result=$(nslookup "$DOMAIN" "$dns" 2>/dev/null | grep -A1 "Name:" | tail -1 | awk '{print $2}')
    [ -n "$result" ] && echo "✅ $result" || echo "❌ Not resolved"
done

echo "🔒 Testing HTTPS connectivity"
curl -I -s --max-time 10 "https://$DOMAIN" && echo "✅ Connected" || echo "❌ Failed"
```

#### Task 1.4.2: Basic file deployment test (1 SP)

```html
<!-- DELIVERABLE: Simple test page -->
<!DOCTYPE html>
<html>
<head><title>Tech Citizen - Test</title></head>
<body><h1>Tech Citizen Landing Page - Coming Soon</h1></body>
</html>
```

**Definition of Done**: DNS resolves correctly, HTTPS works, test page loads from domain

---

## 🎨 Sprint 2: Core Content (Week 2) - 34 SP

### User Story 2.1: Hero Section Implementation

**As a** visitor  
**I want** to immediately understand the value proposition  
**So that** I know if this service fits my needs  

#### Task 2.1.1: Hero component structure (3 SP)

```javascript
// DELIVERABLE: js/components/hero-section.js
import { BaseSection } from './base-section.js';
import { html, css } from 'lit';
import { t } from '../i18n/i18n.js';

export class HeroSection extends BaseSection {
  static styles = [
    super.styles,
    css`
      .hero-gradient {
        background: linear-gradient(135deg, #1e40af 0%, #3b82f6 100%);
      }
      .cta-button {
        @apply bg-amber-500 hover:bg-amber-600 text-white font-bold py-3 px-6 rounded-lg transition-colors;
      }
    `
  ];

  renderContent() {
    return html`
      <div class="hero-gradient text-white py-20">
        <div class="container mx-auto px-4 text-center">
          <h1 class="text-4xl md:text-6xl font-bold mb-4">
            ${t('HERO.TITLE')}
          </h1>
          <h2 class="text-xl md:text-2xl mb-6">
            ${t('HERO.SUBTITLE')}
          </h2>
          <p class="text-lg mb-8">
            ${t('HERO.DESCRIPTION')}
          </p>
          <button 
            class="cta-button"
            @click="${this.handleCTAClick}">
            ${t('HERO.CTA_BUTTON')}
          </button>
          
          <div class="mt-12 grid grid-cols-1 md:grid-cols-3 gap-6 text-sm">
            <div>✓ ${t('HERO.BENEFITS.EXPERIENCE')}</div>
            <div>✓ ${t('HERO.BENEFITS.AGILE')}</div>
            <div>✓ ${t('HERO.BENEFITS.LEADERSHIP')}</div>
          </div>
        </div>
      </div>
    `;
  }
  
  handleCTAClick() {
    this.trackEvent('hero_cta_click', { location: 'hero_section' });
    // Scroll to contact form
    document.querySelector('contact-form')?.scrollIntoView({ behavior: 'smooth' });
  }
}

customElements.define('hero-section', HeroSection);
```

#### Task 2.1.2: Hero responsive design (2 SP)

```css
/* DELIVERABLE: css/custom.css - Hero responsive styles */
@media (max-width: 768px) {
  .hero-gradient h1 { @apply text-3xl; }
  .hero-gradient h2 { @apply text-lg; }
  .hero-gradient .grid { @apply grid-cols-1 gap-4; }
}

@media (min-width: 1024px) {
  .hero-gradient { @apply py-24; }
  .hero-gradient h1 { @apply text-7xl; }
}
```

**Definition of Done**: Hero displays correctly, responsive, CTA button works, analytics tracking

---

### User Story 2.2: Services Grid Implementation  

**As a** potential client  
**I want** to see available services clearly  
**So that** I can understand if they match my needs  

#### Task 2.2.1: Services data model (2 SP)

```javascript
// DELIVERABLE: js/data/services-data.js
export const servicesData = [
  {
    id: 'software-dev',
    icon: '💻',
    titleKey: 'SERVICES.SOFTWARE_DEV.TITLE',
    descriptionKey: 'SERVICES.SOFTWARE_DEV.DESCRIPTION',
    technologies: ['Node.js', 'React', 'TypeScript'],
    featured: true
  },
  {
    id: 'training',
    icon: '🎓',
    titleKey: 'SERVICES.TRAINING.TITLE', 
    descriptionKey: 'SERVICES.TRAINING.DESCRIPTION',
    technologies: ['Agile', 'Scrum', 'Emotional Intelligence'],
    featured: true
  },
  {
    id: 'onboarding',
    icon: '🚀',
    titleKey: 'SERVICES.ONBOARDING.TITLE',
    descriptionKey: 'SERVICES.ONBOARDING.DESCRIPTION',
    technologies: ['Integration', 'Mentoring', 'Best Practices'],
    featured: false
  },
  {
    id: 'agile',
    icon: '⚡',
    titleKey: 'SERVICES.AGILE.TITLE',
    descriptionKey: 'SERVICES.AGILE.DESCRIPTION', 
    technologies: ['Kanban', 'Scrum', 'XP'],
    featured: true
  },
  {
    id: 'fractional-cto',
    icon: '🎯',
    titleKey: 'SERVICES.CTO.TITLE',
    descriptionKey: 'SERVICES.CTO.DESCRIPTION',
    technologies: ['Leadership', 'Strategy', 'Architecture'],
    featured: true
  },
  {
    id: 'emotional-intelligence',
    icon: '🧠',
    titleKey: 'SERVICES.EMOTIONAL.TITLE',
    descriptionKey: 'SERVICES.EMOTIONAL.DESCRIPTION',
    technologies: ['Psychology', 'Team Dynamics', 'Conflict Resolution'],
    featured: false
  }
];
```

#### Task 2.2.2: Services grid component (4 SP)

```javascript
// DELIVERABLE: js/components/services-grid.js
import { BaseSection } from './base-section.js';
import { html, css } from 'lit';
import { t } from '../i18n/i18n.js';
import { servicesData } from '../data/services-data.js';

export class ServicesGrid extends BaseSection {
  static properties = {
    services: { type: Array },
    showAll: { type: Boolean }
  };

  constructor() {
    super();
    this.services = servicesData;
    this.showAll = false;
  }

  get displayedServices() {
    return this.showAll ? this.services : this.services.filter(s => s.featured);
  }

  static styles = [
    super.styles,
    css`
      .service-card {
        @apply bg-white rounded-lg shadow-md hover:shadow-lg transition-shadow p-6;
        border-top: 4px solid #3b82f6;
      }
      .service-icon {
        @apply text-4xl mb-4 block;
      }
      .tech-badge {
        @apply px-2 py-1 bg-blue-100 text-blue-800 text-xs rounded mr-2 mb-2;
      }
    `
  ];

  renderService(service) {
    return html`
      <div class="service-card" @click="${() => this.trackServiceClick(service.id)}">
        <span class="service-icon">${service.icon}</span>
        <h3 class="font-bold text-lg mb-2">${t(service.titleKey)}</h3>
        <p class="text-gray-600 mb-4">${t(service.descriptionKey)}</p>
        <div class="flex flex-wrap">
          ${service.technologies.map(tech => html`
            <span class="tech-badge">${tech}</span>
          `)}
        </div>
      </div>
    `;
  }

  renderContent() {
    return html`
      <div class="bg-gray-50">
        <h2 class="text-3xl font-bold text-center mb-12">${t('SERVICES.TITLE')}</h2>
        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
          ${this.displayedServices.map(service => this.renderService(service))}
        </div>
        ${!this.showAll ? html`
          <div class="text-center mt-8">
            <button 
              @click="${this.toggleShowAll}"
              class="bg-blue-600 text-white px-6 py-2 rounded hover:bg-blue-700">
              Mostra tutti i servizi
            </button>
          </div>
        ` : ''}
      </div>
    `;
  }

  toggleShowAll() {
    this.showAll = true;
    this.trackEvent('services_expand', { total_services: this.services.length });
  }

  trackServiceClick(serviceId) {
    this.trackEvent('service_click', { service: serviceId });
  }
}

customElements.define('services-grid', ServicesGrid);
```

#### Task 2.2.3: Services responsive grid (2 SP)

```css
/* DELIVERABLE: Services responsive styles */
@media (max-width: 768px) {
  .services-grid { @apply grid-cols-1 gap-4; }
  .service-card { @apply p-4; }
}

@media (min-width: 769px) and (max-width: 1024px) {
  .services-grid { @apply grid-cols-2 gap-6; }
}

@media (min-width: 1025px) {
  .services-grid { @apply grid-cols-3 gap-8; }
}
```

**Definition of Done**: 6 services display correctly, responsive grid, featured/all toggle works

---

### User Story 2.3: Projects Section with Empty State

**As a** potential client  
**I want** to see previous work examples  
**So that** I can evaluate expertise and credibility  

#### Task 2.3.1: Projects data model with edge cases (3 SP)

```javascript
// DELIVERABLE: js/data/projects-data.js
export const projectsData = [
  // START WITH EMPTY ARRAY FOR TESTING
  // {
  //   id: "erp-modernization",
  //   title: "ERP Modernization Platform",
  //   description: "Migrazione completa sistema legacy ERP verso architettura microservizi",
  //   icon: "🏢", // Optional
  //   technologies: ["Node.js", "React", "PostgreSQL", "Docker"],
  //   category: "Enterprise Software",
  //   duration: "8 mesi",
  //   links: [ // Optional array
  //     { type: "case_study", url: "/case-studies/erp", label: "Case Study" },
  //     { type: "demo", url: "https://demo.example.com", label: "Demo Live" }
  //   ],
  //   status: "completed",
  //   featured: true,
  //   client: "Azienda Manifatturiera (NDA)",
  //   results: [
  //     "80% riduzione tempi elaborazione",
  //     "99.9% uptime raggiunto"
  //   ]
  // }
];

// Project data validation
export const validateProject = (project) => {
  const required = ['id', 'title'];
  return required.every(field => project[field]);
};

export const getProjectsWithDefaults = () => {
  return projectsData.filter(validateProject).map(project => ({
    ...project,
    icon: project.icon || null,
    description: project.description || '',
    links: project.links || [],
    technologies: project.technologies || [],
    status: project.status || 'planned'
  }));
};
```

#### Task 2.3.2: Projects component with empty state (4 SP)

```javascript
// DELIVERABLE: js/components/projects-section.js
import { BaseSection } from './base-section.js';
import { html, css } from 'lit';
import { t } from '../i18n/i18n.js';
import { getProjectsWithDefaults } from '../data/projects-data.js';

export class ProjectsSection extends BaseSection {
  static properties = {
    projects: { type: Array },
    loading: { type: Boolean },
    filter: { type: String }
  };

  constructor() {
    super();
    this.projects = [];
    this.loading = true;
    this.filter = 'all';
  }

  async connectedCallback() {
    super.connectedCallback();
    await this.loadProjects();
  }

  async loadProjects() {
    // Simulate API call delay
    await new Promise(resolve => setTimeout(resolve, 500));
    this.projects = getProjectsWithDefaults();
    this.loading = false;
  }

  get filteredProjects() {
    if (this.filter === 'featured') {
      return this.projects.filter(p => p.featured);
    }
    return this.projects;
  }

  get isEmpty() {
    return this.filteredProjects.length === 0;
  }

  static styles = [
    super.styles,
    css`
      .project-card {
        @apply bg-white rounded-lg shadow-md hover:shadow-lg transition-shadow p-6;
      }
      .project-icon {
        @apply text-4xl mb-4 block;
      }
      .project-link {
        @apply inline-flex items-center px-3 py-2 bg-blue-600 text-white text-sm rounded hover:bg-blue-700 transition-colors mr-2 mb-2;
      }
      .empty-state {
        @apply text-center py-12;
      }
      .loading-state {
        @apply text-center py-12 text-gray-500;
      }
    `
  ];

  renderEmptyState() {
    return html`
      <div class="empty-state">
        <div class="text-6xl mb-4">🚀</div>
        <h3 class="text-xl font-semibold mb-2">
          ${t('PROJECTS.EMPTY_STATE.TITLE')}
        </h3>
        <p class="text-gray-600">
          ${t('PROJECTS.EMPTY_STATE.DESCRIPTION')}
        </p>
      </div>
    `;
  }

  renderLoadingState() {
    return html`
      <div class="loading-state">
        <div class="text-2xl mb-4">⏳</div>
        <p>${t('COMMON.LOADING')}</p>
      </div>
    `;
  }

  renderProject(project) {
    return html`
      <div class="project-card">
        ${project.icon ? html`
          <span class="project-icon">${project.icon}</span>
        ` : ''}
        
        <h3 class="font-bold text-lg mb-2">${project.title}</h3>
        
        ${project.description ? html`
          <p class="text-gray-600 mb-4">${project.description}</p>
        ` : ''}
        
        ${project.technologies?.length ? html`
          <div class="mb-4">
            ${project.technologies.map(tech => html`
              <span class="px-2 py-1 bg-blue-100 text-blue-800 text-xs rounded mr-2 mb-2">
                ${tech}
              </span>
            `)}
          </div>
        ` : ''}
        
        ${project.links?.length ? html`
          <div class="flex flex-wrap">
            ${project.links.map(link => html`
              <a href="${link.url}" 
                 class="project-link"
                 target="_blank" 
                 rel="noopener"
                 @click="${() => this.trackProjectLink(project.id, link.type)}">
                ${link.label}
              </a>
            `)}
          </div>
        ` : ''}
      </div>
    `;
  }

  renderContent() {
    if (this.loading) {
      return this.renderLoadingState();
    }

    return html`
      <div class="bg-gray-50">
        <h2 class="text-3xl font-bold text-center mb-12">
          ${t('PROJECTS.TITLE')}
        </h2>
        
        ${this.isEmpty ? this.renderEmptyState() : html`
          <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
            ${this.filteredProjects.map(project => this.renderProject(project))}
          </div>
        `}
      </div>
    `;
  }

  trackProjectLink(projectId, linkType) {
    this.trackEvent('project_link_click', { 
      project: projectId, 
      link_type: linkType 
    });
  }
}

customElements.define('projects-section', ProjectsSection);
```

#### Task 2.3.3: Projects responsive design (2 SP)

```css
/* DELIVERABLE: Projects responsive styles */
@media (max-width: 768px) {
  .projects-grid { @apply grid-cols-1 gap-4; }
  .project-card { @apply p-4; }
  .project-link { @apply text-xs px-2 py-1; }
}

@media (min-width: 769px) and (max-width: 1024px) {
  .projects-grid { @apply grid-cols-2 gap-6; }
}

@media (min-width: 1025px) {
  .projects-grid { @apply grid-cols-3 gap-8; }
}
```

**Definition of Done**: Projects component handles empty state, loading state, optional fields, responsive design

---

### User Story 2.4: About Section

**As a** potential client  
**I want** to understand the consultant's background  
**So that** I can assess credibility and expertise  

#### Task 2.4.1: About component implementation (3 SP)

```javascript
// DELIVERABLE: js/components/about-section.js
import { BaseSection } from './base-section.js';
import { html, css } from 'lit';
import { t } from '../i18n/i18n.js';

export class AboutSection extends BaseSection {
  static styles = [
    super.styles,
    css`
      .about-content {
        @apply max-w-4xl mx-auto text-center;
      }
      .certification {
        @apply flex items-center justify-center mb-4 text-lg;
      }
      .certification-icon {
        @apply mr-3 text-2xl;
      }
      .quote {
        @apply text-xl italic text-gray-700 mt-8 p-6 bg-blue-50 rounded-lg;
      }
    `
  ];

  renderContent() {
    return html`
      <div class="about-content">
        <h2 class="text-3xl font-bold mb-8">${t('ABOUT.TITLE')}</h2>
        
        <p class="text-lg text-gray-700 mb-8">
          ${t('ABOUT.DESCRIPTION')}
        </p>
        
        <div class="grid grid-cols-1 md:grid-cols-2 gap-6 mb-8">
          <div class="certification">
            <span class="certification-icon">🏆</span>
            ${t('ABOUT.CERTIFICATIONS.SCRUM')}
          </div>
          <div class="certification">
            <span class="certification-icon">🧠</span>
            ${t('ABOUT.CERTIFICATIONS.EMOTIONAL')}
          </div>
          <div class="certification">
            <span class="certification-icon">⚡</span>
            ${t('ABOUT.CERTIFICATIONS.CTO')}
          </div>
          <div class="certification">
            <span class="certification-icon">🎓</span>
            ${t('ABOUT.CERTIFICATIONS.TRAINER')}
          </div>
        </div>
        
        <blockquote class="quote">
          "${t('ABOUT.QUOTE')}"
        </blockquote>
      </div>
    `;
  }

  connectedCallback() {
    super.connectedCallback();
    this.trackEvent('about_section_view');
  }
}

customElements.define('about-section', AboutSection);
```

**Definition of Done**: About section displays, certifications shown, responsive layout, analytics tracking

---

### User Story 2.5: Contact Form

**As a** potential client  
**I want** to easily contact the consultant  
**So that** I can start a business conversation  

#### Task 2.5.1: Contact form component (5 SP)

```javascript
// DELIVERABLE: js/components/contact-form.js
import { BaseSection } from './base-section.js';
import { html, css } from 'lit';
import { t } from '../i18n/i18n.js';

export class ContactForm extends BaseSection {
  static properties = {
    formData: { type: Object },
    submitting: { type: Boolean },
    submitted: { type: Boolean },
    errors: { type: Object }
  };

  constructor() {
    super();
    this.formData = {
      name: '',
      company: '',
      email: '',
      role: '',
      challenge: ''
    };
    this.submitting = false;
    this.submitted = false;
    this.errors = {};
  }

  static styles = [
    super.styles,
    css`
      .form-group {
        @apply mb-6;
      }
      .form-label {
        @apply block text-sm font-medium text-gray-700 mb-2;
      }
      .form-input {
        @apply w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500;
      }
      .form-error {
        @apply text-red-600 text-sm mt-1;
      }
      .submit-button {
        @apply w-full bg-amber-500 hover:bg-amber-600 text-white font-bold py-3 px-6 rounded-lg transition-colors disabled:opacity-50;
      }
      .success-message {
        @apply bg-green-100 border border-green-400 text-green-700 px-4 py-3 rounded mb-4;
      }
    `
  ];

  validateForm() {
    const errors = {};
    
    if (!this.formData.name.trim()) {
      errors.name = 'Nome è obbligatorio';
    }
    
    if (!this.formData.email.trim()) {
      errors.email = 'Email è obbligatoria';
    } else if (!/\S+@\S+\.\S+/.test(this.formData.email)) {
      errors.email = 'Email non valida';
    }
    
    if (!this.formData.challenge.trim()) {
      errors.challenge = 'Descrivi la tua sfida';
    }
    
    this.errors = errors;
    return Object.keys(errors).length === 0;
  }

  handleInputChange(field, event) {
    this.formData = {
      ...this.formData,
      [field]: event.target.value
    };
    
    // Clear error when user starts typing
    if (this.errors[field]) {
      this.errors = { ...this.errors };
      delete this.errors[field];
    }
  }

  async handleSubmit(event) {
    event.preventDefault();
    
    if (!this.validateForm()) {
      this.trackEvent('form_validation_error', { errors: Object.keys(this.errors) });
      return;
    }
    
    this.submitting = true;
    this.trackEvent('form_submit_start', { email: this.formData.email });
    
    try {
      // Simulate API call
      await new Promise(resolve => setTimeout(resolve, 2000));
      
      // In production, send to actual endpoint
      console.log('Form submitted:', this.formData);
      
      this.submitted = true;
      this.trackEvent('form_submit_success', { 
        company: this.formData.company,
        role: this.formData.role 
      });
      
    } catch (error) {
      console.error('Form submission error:', error);
      this.errors = { submit: 'Errore durante l\'invio. Riprova.' };
      this.trackEvent('form_submit_error', { error: error.message });
    } finally {
      this.submitting = false;
    }
  }

  renderForm() {
    return html`
      <form @submit="${this.handleSubmit}" class="max-w-lg mx-auto">
        <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
          <div class="form-group">
            <label class="form-label">${t('CONTACT.FORM.NAME')}</label>
            <input 
              type="text"
              class="form-input ${this.errors.name ? 'border-red-500' : ''}"
              .value="${this.formData.name}"
              @input="${(e) => this.handleInputChange('name', e)}"
              required>
            ${this.errors.name ? html`<div class="form-error">${this.errors.name}</div>` : ''}
          </div>
          
          <div class="form-group">
            <label class="form-label">${t('CONTACT.FORM.COMPANY')}</label>
            <input 
              type="text"
              class="form-input"
              .value="${this.formData.company}"
              @input="${(e) => this.handleInputChange('company', e)}">
          </div>
        </div>
        
        <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
          <div class="form-group">
            <label class="form-label">${t('CONTACT.FORM.EMAIL')}</label>
            <input 
              type="email"
              class="form-input ${this.errors.email ? 'border-red-500' : ''}"
              .value="${this.formData.email}"
              @input="${(e) => this.handleInputChange('email', e)}"
              required>
            ${this.errors.email ? html`<div class="form-error">${this.errors.email}</div>` : ''}
          </div>
          
          <div class="form-group">
            <label class="form-label">${t('CONTACT.FORM.ROLE')}</label>
            <input 
              type="text"
              class="form-input"
              .value="${this.formData.role}"
              @input="${(e) => this.handleInputChange('role', e)}">
          </div>
        </div>
        
        <div class="form-group">
          <label class="form-label">${t('CONTACT.FORM.CHALLENGE')}</label>
          <textarea 
            class="form-input ${this.errors.challenge ? 'border-red-500' : ''}"
            rows="4"
            .value="${this.formData.challenge}"
            @input="${(e) => this.handleInputChange('challenge', e)}"
            required></textarea>
          ${this.errors.challenge ? html`<div class="form-error">${this.errors.challenge}</div>` : ''}
        </div>
        
        ${this.errors.submit ? html`<div class="form-error mb-4">${this.errors.submit}</div>` : ''}
        
        <button 
          type="submit"
          class="submit-button"
          ?disabled="${this.submitting}">
          ${this.submitting ? t('COMMON.LOADING') : t('CONTACT.FORM.SUBMIT')}
        </button>
      </form>
    `;
  }

  renderSuccessMessage() {
    return html`
      <div class="success-message text-center">
        <h3 class="font-bold text-lg mb-2">Grazie per il tuo interesse!</h3>
        <p>Ti contatteremo entro 24 ore per discutere la tua sfida.</p>
      </div>
    `;
  }

  renderContent() {
    return html`
      <div class="bg-white">
        <h2 class="text-3xl font-bold text-center mb-12">
          ${t('CONTACT.TITLE')}
        </h2>
        
        ${this.submitted ? this.renderSuccessMessage() : this.renderForm()}
        
        <div class="text-center mt-12 space-y-2">
          <p>📧 ${t('CONTACT.DIRECT.EMAIL')}</p>
          <p>💼 ${t('CONTACT.DIRECT.LINKEDIN')}</p>
          <p>📅 ${t('CONTACT.DIRECT.CALENDAR')}</p>
        </div>
      </div>
    `;
  }
}

customElements.define('contact-form', ContactForm);
```

#### Task 2.5.2: Form validation and UX (2 SP)

```javascript
// DELIVERABLE: Enhanced form validation
class FormValidator {
  static validateEmail(email) {
    const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
    return emailRegex.test(email);
  }
  
  static validateRequired(value, fieldName) {
    if (!value || !value.trim()) {
      return `${fieldName} è obbligatorio`;
    }
    return null;
  }
  
  static validateLength(value, min, max, fieldName) {
    if (value.length < min) {
      return `${fieldName} deve essere almeno ${min} caratteri`;
    }
    if (value.length > max) {
      return `${fieldName} non può superare ${max} caratteri`;
    }
    return null;
  }
}
```

**Definition of Done**: Form submits, validates input, shows success/error states, responsive design

---

## 🎨 Sprint 3: Interactive Features (Week 3) - 21 SP

### User Story 3.1: Technology Carousel

**As a** technical decision maker  
**I want** to see the technology stack  
**So that** I can assess technical compatibility  

#### Task 3.1.1: Technology data model (2 SP)

```javascript
// DELIVERABLE: js/data/tech-stack-data.js
export const techStackData = {
  "Runtime & Languages": [
    { name: "Node.js", icon: "🟢", category: "runtime" },
    { name: "JavaScript", icon: "🟨", category: "language" },
    { name: "TypeScript", icon: "🔷", category: "language" }
  ],
  "Backend Frameworks": [
    { name: "NestJS", icon: "🦅", category: "framework" },
    { name: "Express.js", icon: "⚡", category: "framework" },
    { name: "Fastify", icon: "🚀", category: "framework" },
    { name: "Platformatic", icon: "🏗️", category: "framework" }
  ],
  "Frontend": [
    { name: "LitElement", icon: "🔥", category: "framework" },
    { name: "React", icon: "⚛️", category: "framework" },
    { name: "Tailwind CSS", icon: "🎨", category: "styling" }
  ],
  "Database & Cache": [
    { name: "Redis", icon: "🔴", category: "cache" },
    { name: "RedisSearch", icon: "🔍", category: "search" }
  ],
  "Monitoring & Observability": [
    { name: "Elasticsearch", icon: "🔍", category: "search" },
    { name: "Kibana", icon: "📊", category: "visualization" },
    { name: "Logstash", icon: "📝", category: "processing" },
    { name: "Filebeat", icon: "📄", category: "collection" },
    { name: "Loki", icon: "🪵", category: "logging" }
  ],
  "DevOps & Infrastructure": [
    { name: "Docker", icon: "🐳", category: "container" },
    { name: "Docker Swarm", icon: "🐝", category: "orchestration" },
    { name: "Ansible", icon: "🤖", category: "automation" },
    { name: "Jenkins", icon: "👷", category: "ci_cd" }
  ],
  "Message Queue": [
    { name: "RabbitMQ", icon: "🐰", category: "messaging" }
  ],
  "Git Workflows": [
    { name: "Git Flow", icon: "🌊", category: "workflow" },
    { name: "Trunk Based", icon: "🌳", category: "workflow" }
  ],
  "Methodologies": [
    { name: "DDD", icon: "🏗️", category: "architecture" },
    { name: "BDD", icon: "🎯", category: "testing" },
    { name: "TDD", icon: "🧪", category: "testing" },
    { name: "Kanban", icon: "📋", category: "agile" },
    { name: "Scrum", icon: "🏃", category: "agile" },
    { name: "XP", icon: "⚡", category: "agile" }
  ]
};

export const getAllTechnologies = () => {
  return Object.values(techStackData).flat();
};

export const getTechnologiesByCategory = (category) => {
  return techStackData[category] || [];
};
```

#### Task 3.1.2: Setup Swiper.js carousel library (1 SP)

```html
<!-- DELIVERABLE: Swiper.js integration -->
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/swiper@11/swiper-bundle.min.css">
<script src="https://cdn.jsdelivr.net/npm/swiper@11/swiper-bundle.min.js"></script>
```

#### Task 3.1.3: Tech carousel component (5 SP)

```javascript
// DELIVERABLE: js/components/tech-carousel.js
import { BaseSection } from './base-section.js';
import { html, css } from 'lit';
import { t } from '../i18n/i18n.js';
import { techStackData, getAllTechnologies } from '../data/tech-stack-data.js';

export class TechCarousel extends BaseSection {
  static properties = {
    selectedCategory: { type: String },
    technologies: { type: Array },
    autoplay: { type: Boolean }
  };

  constructor() {
    super();
    this.selectedCategory = 'all';
    this.technologies = getAllTechnologies();
    this.autoplay = true;
    this.swiper = null;
  }

  async firstUpdated() {
    await this.initSwiper();
  }

  async initSwiper() {
    // Wait for Swiper to be available
    while (typeof Swiper === 'undefined') {
      await new Promise(resolve => setTimeout(resolve, 100));
    }

    const swiperContainer = this.shadowRoot.querySelector('.swiper');
    if (swiperContainer) {
      this.swiper = new Swiper(swiperContainer, {
        modules: [Swiper.Autoplay, Swiper.Pagination, Swiper.Navigation],
        slidesPerView: 2,
        spaceBetween: 10,
        autoplay: this.autoplay ? {
          delay: 3000,
          disableOnInteraction: false,
        } : false,
        pagination: {
          el: '.swiper-pagination',
          clickable: true,
        },
        navigation: {
          nextEl: '.swiper-button-next',
          prevEl: '.swiper-button-prev',
        },
        breakpoints: {
          640: {
            slidesPerView: 3,
            spaceBetween: 20,
          },
          768: {
            slidesPerView: 4,
            spaceBetween: 30,
          },
          1024: {
            slidesPerView: 6,
            spaceBetween: 40,
          },
        },
        on: {
          slideChange: () => {
            this.trackEvent('tech_carousel_slide', { 
              category: this.selectedCategory 
            });
          }
        }
      });
    }
  }

  get categories() {
    return ['all', ...Object.keys(techStackData)];
  }

  get displayedTechnologies() {
    if (this.selectedCategory === 'all') {
      return getAllTechnologies();
    }
    return techStackData[this.selectedCategory] || [];
  }

  handleCategoryChange(category) {
    this.selectedCategory = category;
    this.technologies = this.displayedTechnologies;
    this.trackEvent('tech_category_change', { category });
    
    // Update swiper
    if (this.swiper) {
      this.swiper.update();
      this.swiper.slideTo(0);
    }
  }

  handleTechClick(tech) {
    this.trackEvent('tech_click', { 
      technology: tech.name, 
      category: tech.category 
    });
  }

  static styles = [
    super.styles,
    css`
      .category-tabs {
        @apply flex flex-wrap justify-center gap-2 mb-8;
      }
      .category-tab {
        @apply px-4 py-2 rounded-full text-sm transition-colors cursor-pointer;
      }
      .category-tab.active {
        @apply bg-blue-600 text-white;
      }
      .category-tab:not(.active) {
        @apply bg-gray-200 text-gray-700 hover:bg-gray-300;
      }
      .tech-card {
        @apply bg-white rounded-lg shadow-md p-4 text-center hover:shadow-lg transition-shadow cursor-pointer;
        min-height: 120px;
        display: flex;
        flex-direction: column;
        justify-content: center;
      }
      .tech-icon {
        @apply text-3xl mb-2;
      }
      .tech-name {
        @apply font-medium text-sm;
      }
      .swiper {
        @apply w-full;
        padding: 20px 0;
      }
      .swiper-slide {
        @apply h-auto;
      }
      .swiper-button-next,
      .swiper-button-prev {
        color: #3b82f6;
      }
      .swiper-pagination-bullet-active {
        background: #3b82f6;
      }
    `
  ];

  renderTechnology(tech) {
    return html`
      <div class="swiper-slide">
        <div class="tech-card" @click="${() => this.handleTechClick(tech)}">
          <div class="tech-icon">${tech.icon}</div>
          <div class="tech-name">${tech.name}</div>
        </div>
      </div>
    `;
  }

  renderContent() {
    return html`
      <div class="bg-gray-50">
        <h2 class="text-3xl font-bold text-center mb-8">
          ${t('TECH.TITLE')}
        </h2>
        
        <!-- Category Tabs -->
        <div class="category-tabs">
          ${this.categories.map(category => html`
            <button 
              class="category-tab ${this.selectedCategory === category ? 'active' : ''}"
              @click="${() => this.handleCategoryChange(category)}">
              ${category === 'all' ? 'Tutte' : t(`TECH.CATEGORIES.${category.toUpperCase().replace(/ & /g, '_').replace(/ /g, '_')}`)}
            </button>
          `)}
        </div>
        
        <!-- Swiper Carousel -->
        <div class="swiper">
          <div class="swiper-wrapper">
            ${this.displayedTechnologies.map(tech => this.renderTechnology(tech))}
          </div>
          <div class="swiper-pagination"></div>
          <div class="swiper-button-prev"></div>
          <div class="swiper-button-next"></div>
        </div>
        
        <!-- Category Descriptions -->
        <div class="text-center mt-8 grid grid-cols-1 md:grid-cols-3 gap-4 text-sm text-gray-600">
          <div>📊 Backend • Frontend</div>
          <div>📈 Monitoring • DevOps</div>
          <div>🔄 Agile • Methodologies</div>
        </div>
      </div>
    `;
  }
}

customElements.define('tech-carousel', TechCarousel);
```

#### Task 3.1.4: Carousel responsive design (2 SP)

```css
/* DELIVERABLE: Carousel responsive styles */
@media (max-width: 640px) {
  .tech-carousel .swiper {
    padding: 10px 0;
  }
  .tech-card {
    min-height: 100px;
    padding: 12px;
  }
  .tech-icon {
    font-size: 1.5rem;
  }
  .category-tabs {
    gap: 4px;
  }
  .category-tab {
    padding: 6px 12px;
    font-size: 0.75rem;
  }
}

@media (min-width: 1024px) {
  .tech-card {
    min-height: 140px;
    padding: 20px;
  }
  .tech-icon {
    font-size: 2.5rem;
  }
}
```

**Definition of Done**: Tech carousel works, responsive, category filtering, analytics tracking

---

### User Story 3.2: Navigation & Smooth Scrolling

**As a** user  
**I want** smooth navigation between sections  
**So that** I can easily explore the page  

#### Task 3.2.1: Navigation component (3 SP)

```javascript
// DELIVERABLE: js/components/navigation.js
import { LitElement, html, css } from 'lit';
import { t } from '../i18n/i18n.js';

export class Navigation extends LitElement {
  static properties = {
    isSticky: { type: Boolean },
    activeSection: { type: String }
  };

  constructor() {
    super();
    this.isSticky = false;
    this.activeSection = 'hero';
    this.sections = [
      { id: 'hero', labelKey: 'HERO.TITLE' },
      { id: 'services', labelKey: 'SERVICES.TITLE' },
      { id: 'tech', labelKey: 'TECH.TITLE' },
      { id: 'projects', labelKey: 'PROJECTS.TITLE' },
      { id: 'about', labelKey: 'ABOUT.TITLE' },
      { id: 'contact', labelKey: 'CONTACT.TITLE' }
    ];
  }

  connectedCallback() {
    super.connectedCallback();
    this.setupScrollListener();
    this.setupIntersectionObserver();
  }

  setupScrollListener() {
    window.addEventListener('scroll', () => {
      this.isSticky = window.scrollY > 100;
    });
  }

  setupIntersectionObserver() {
    const observer = new IntersectionObserver(
      (entries) => {
        entries.forEach(entry => {
          if (entry.isIntersecting) {
            this.activeSection = entry.target.id;
          }
        });
      },
      { threshold: 0.3, rootMargin: '-100px 0px' }
    );

    // Observe all sections
    this.sections.forEach(section => {
      const element = document.getElementById(section.id);
      if (element) observer.observe(element);
    });
  }

  scrollToSection(sectionId) {
    const element = document.getElementById(sectionId);
    if (element) {
      element.scrollIntoView({ 
        behavior: 'smooth',
        block: 'start'
      });
      
      // Track navigation
      this.trackEvent('navigation_click', { section: sectionId });
    }
  }

  static styles = css`
    :host {
      display: block;
      position: fixed;
      top: 0;
      left: 0;
      right: 0;
      z-index: 1000;
      transition: all 0.3s ease;
    }
    
    nav {
      @apply bg-white shadow-md px-4 py-3;
    }
    
    .nav-container {
      @apply container mx-auto flex items-center justify-between;
    }
    
    .logo {
      @apply text-xl font-bold text-blue-600;
    }
    
    .nav-menu {
      @apply hidden md:flex space-x-6;
    }
    
    .nav-link {
      @apply text-gray-700 hover:text-blue-600 transition-colors cursor-pointer;
    }
    
    .nav-link.active {
      @apply text-blue-600 font-medium;
    }
    
    .mobile-menu-button {
      @apply md:hidden text-gray-700;
    }
    
    :host(.sticky) nav {
      @apply backdrop-blur-sm bg-white/95;
    }
  `;

  render() {
    return html`
      <nav>
        <div class="nav-container">
          <div class="logo">Tech Citizen</div>
          
          <div class="nav-menu">
            ${this.sections.map(section => html`
              <button 
                class="nav-link ${this.activeSection === section.id ? 'active' : ''}"
                @click="${() => this.scrollToSection(section.id)}">
                ${t(section.labelKey)}
              </button>
            `)}
          </div>
          
          <button class="mobile-menu-button">
            ☰
          </button>
        </div>
      </nav>
    `;
  }

  trackEvent(eventName, data) {
    console.log('Track:', eventName, data);
  }
}

customElements.define('app-navigation', Navigation);
```

#### Task 3.2.2: Smooth scroll polyfill (1 SP)

```javascript
// DELIVERABLE: js/utils/smooth-scroll.js
export class SmoothScrollUtils {
  static scrollToElement(elementId, offset = 80) {
    const element = document.getElementById(elementId);
    if (!element) return;

    const elementPosition = element.getBoundingClientRect().top;
    const offsetPosition = elementPosition + window.pageYOffset - offset;

    window.scrollTo({
      top: offsetPosition,
      behavior: 'smooth'
    });
  }

  static scrollToTop() {
    window.scrollTo({
      top: 0,
      behavior: 'smooth'
    });
  }
}
```

**Definition of Done**: Navigation is sticky, active states work, smooth scrolling works

---

### User Story 3.3: Performance Optimization

**As a** user  
**I want** fast page loading  
**So that** I don't wait for content  

#### Task 3.3.1: Image optimization and lazy loading (2 SP)

```javascript
// DELIVERABLE: js/utils/lazy-loading.js
export class LazyLoadUtils {
  static observeImages() {
    const imageObserver = new IntersectionObserver((entries, observer) => {
      entries.forEach(entry => {
        if (entry.isIntersecting) {
          const img = entry.target;
          img.src = img.dataset.src;
          img.classList.remove('lazy');
          observer.unobserve(img);
        }
      });
    });

    document.querySelectorAll('img[data-src]').forEach(img => {
      imageObserver.observe(img);
    });
  }

  static observeComponents() {
    const componentObserver = new IntersectionObserver((entries) => {
      entries.forEach(entry => {
        if (entry.isIntersecting) {
          const component = entry.target;
          component.classList.add('loaded');
        }
      });
    }, { threshold: 0.1 });

    document.querySelectorAll('[data-lazy-component]').forEach(component => {
      componentObserver.observe(component);
    });
  }
}
```

#### Task 3.3.2: Component loading optimization (2 SP)

```javascript
// DELIVERABLE: js/utils/component-loader.js
export class ComponentLoader {
  static async loadComponent(componentName) {
    try {
      const module = await import(`../components/${componentName}.js`);
      console.log(`Component ${componentName} loaded`);
      return module;
    } catch (error) {
      console.error(`Failed to load component ${componentName}:`, error);
      return null;
    }
  }

  static async loadComponentsOnDemand() {
    const observer = new IntersectionObserver(async (entries) => {
      entries.forEach(async (entry) => {
        if (entry.isIntersecting) {
          const componentName = entry.target.dataset.component;
          if (componentName) {
            await this.loadComponent(componentName);
            observer.unobserve(entry.target);
          }
        }
      });
    }, { rootMargin: '100px' });

    document.querySelectorAll('[data-component]').forEach(element => {
      observer.observe(element);
    });
  }
}
```

#### Task 3.3.3: Analytics integration (3 SP)

```javascript
// DELIVERABLE: js/utils/analytics.js
class AnalyticsService {
  constructor() {
    this.events = [];
    this.sessionId = this.generateSessionId();
    this.initialized = false;
  }

  generateSessionId() {
    return `session_${Date.now()}_${Math.random().toString(36).substr(2, 9)}`;
  }

  init() {
    if (this.initialized) return;
    
    this.trackPageView();
    this.setupAutoTracking();
    this.initialized = true;
  }

  track(eventName, properties = {}) {
    const event = {
      name: eventName,
      properties: {
        ...properties,
        timestamp: new Date().toISOString(),
        sessionId: this.sessionId,
        url: window.location.href,
        userAgent: navigator.userAgent
      }
    };

    this.events.push(event);
    console.log('Analytics event:', event);

    // In production, send to analytics service
    this.sendToAnalytics(event);
  }

  trackPageView() {
    this.track('page_view', {
      title: document.title,
      path: window.location.pathname
    });
  }

  setupAutoTracking() {
    // Track scroll depth
    let maxScroll = 0;
    window.addEventListener('scroll', () => {
      const scrollPercent = Math.round(
        (window.scrollY / (document.body.scrollHeight - window.innerHeight)) * 100
      );
      
      if (scrollPercent > maxScroll) {
        maxScroll = scrollPercent;
        if (scrollPercent % 25 === 0) {
          this.track('scroll_depth', { depth: scrollPercent });
        }
      }
    });

    // Track time on page
    let startTime = Date.now();
    window.addEventListener('beforeunload', () => {
      const timeOnPage = Math.round((Date.now() - startTime) / 1000);
      this.track('time_on_page', { seconds: timeOnPage });
    });
  }

  async sendToAnalytics(event) {
    try {
      // Simulate API call
      if (process.env.NODE_ENV === 'production') {
        await fetch('/api/analytics', {
          method: 'POST',
          headers: { 'Content-Type': 'application/json' },
          body: JSON.stringify(event)
        });
      }
    } catch (error) {
      console.error('Analytics error:', error);
    }
  }
}

export const analytics = new AnalyticsService();
export const track = (eventName, properties) => analytics.track(eventName, properties);
```

**Definition of Done**: Components load efficiently, analytics tracking works, performance optimized

---

## 🚀 Sprint 4: Production & Polish (Week 4) - 13 SP

### User Story 4.1: Production Deployment

**As a** business owner  
**I want** the site live on tech-citizen.me  
**So that** customers can find and contact us  

#### Task 4.1.1: Production build optimization (3 SP)

```javascript
// DELIVERABLE: js/utils/production-optimizer.js
export class ProductionOptimizer {
  static async optimizeAssets() {
    // Preload critical resources
    const criticalResources = [
      'https://cdn.tailwindcss.com',
      './css/custom.css',
      './js/i18n/locales/it.json'
    ];

    criticalResources.forEach(resource => {
      const link = document.createElement('link');
      link.rel = 'preload';
      link.href = resource;
      link.as = resource.endsWith('.css') ? 'style' : 'fetch';
      document.head.appendChild(link);
    });
  }

  static enableServiceWorker() {
    if ('serviceWorker' in navigator) {
      navigator.serviceWorker.register('./sw.js')
        .then(registration => {
          console.log('SW registered:', registration);
        })
        .catch(error => {
          console.log('SW registration failed:', error);
        });
    }
  }

  static optimizeImages() {
    // Implement WebP support detection
    const webpSupported = document.createElement('canvas')
      .toDataURL('image/webp').indexOf('data:image/webp') === 0;
    
    if (webpSupported) {
      document.documentElement.classList.add('webp-supported');
    }
  }
}
```

#### Task 4.1.2: Service worker for caching (2 SP)

```javascript
// DELIVERABLE: sw.js
const CACHE_NAME = 'tech-citizen-v1';
const urlsToCache = [
  '/',
  '/css/custom.css',
  '/js/main.js',
  '/js/i18n/locales/it.json',
  'https://cdn.tailwindcss.com',
  'https://cdn.skypack.dev/lit@2'
];

self.addEventListener('install', event => {
  event.waitUntil(
    caches.open(CACHE_NAME)
      .then(cache => cache.addAll(urlsToCache))
  );
});

self.addEventListener('fetch', event => {
  event.respondWith(
    caches.match(event.request)
      .then(response => {
        // Return cached version or fetch from network
        return response || fetch(event.request);
      }
    )
  );
});
```

#### Task 4.1.3: SEO optimization (2 SP)

```html
<!-- DELIVERABLE: Enhanced SEO meta tags -->
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  
  <!-- SEO Meta Tags -->
  <title>Tech Citizen - Consulenza Software Enterprise | Fractional CTO</title>
  <meta name="description" content="Consulenza software enterprise, Fractional CTO, formazione Agile e transformation digitale. Expertise in Node.js, React, metodologie Scrum.">
  <meta name="keywords" content="fractional cto, consulenza software, agile transformation, formazione enterprise, nodejs, react">
  <meta name="author" content="Tech Citizen">
  
  <!-- Open Graph -->
  <meta property="og:title" content="Tech Citizen - Consulenza Software Enterprise">
  <meta property="og:description" content="Fractional CTO e consulenza Agile per scale-up e enterprise">
  <meta property="og:type" content="website">
  <meta property="og:url" content="https://tech-citizen.me">
  <meta property="og:image" content="https://tech-citizen.me/assets/og-image.jpg">
  
  <!-- Twitter Card -->
  <meta name="twitter:card" content="summary_large_image">
  <meta name="twitter:title" content="Tech Citizen - Consulenza Software Enterprise">
  <meta name="twitter:description" content="Fractional CTO e consulenza Agile per scale-up e enterprise">
  
  <!-- Structured Data -->
  <script type="application/ld+json">
  {
    "@context": "https://schema.org",
    "@type": "ProfessionalService",
    "name": "Tech Citizen",
    "description": "Consulenza software enterprise e Fractional CTO",
    "url": "https://tech-citizen.me",
    "sameAs": [
      "https://linkedin.com/in/tech-citizen"
    ],
    "serviceType": "Software Consulting",
    "areaServed": "Italy",
    "hasOfferCatalog": {
      "@type": "OfferCatalog",
      "name": "Servizi Consulenza",
      "itemListElement": [
        {
          "@type": "Offer",
          "itemOffered": {
            "@type": "Service", 
            "name": "Fractional CTO"
          }
        },
        {
          "@type": "Offer",
          "itemOffered": {
            "@type": "Service",
            "name": "Formazione Agile"
          }
        }
      ]
    }
  }
  </script>
</head>
```

**Definition of Done**: Site deployed to production, SEO optimized, service worker caching

---

### User Story 4.2: Testing & Quality Assurance

**As a** developer  
**I want** comprehensive tests  
**So that** the site works reliably  

#### Task 4.2.1: Component unit tests (3 SP)

```javascript
// DELIVERABLE: tests/components.test.js
import { expect } from '@esm-bundle/chai';
import { fixture, html } from '@open-wc/testing';
import '../js/components/hero-section.js';
import '../js/components/contact-form.js';

describe('HeroSection', () => {
  it('renders with correct title', async () => {
    const el = await fixture(html`<hero-section></hero-section>`);
    const title = el.shadowRoot.querySelector('h1');
    expect(title).to.exist;
    expect(title.textContent).to.include('Trasformazione Agile');
  });

  it('handles CTA click correctly', async () => {
    const el = await fixture(html`<hero-section></hero-section>`);
    const button = el.shadowRoot.querySelector('.cta-button');
    
    let eventFired = false;
    el.addEventListener('cta-click', () => eventFired = true);
    
    button.click();
    expect(eventFired).to.be.true;
  });
});

describe('ContactForm', () => {
  it('validates required fields', async () => {
    const el = await fixture(html`<contact-form></contact-form>`);
    
    // Test empty form submission
    const form = el.shadowRoot.querySelector('form');
    const submitEvent = new Event('submit');
    form.dispatchEvent(submitEvent);
    
    expect(el.errors.name).to.exist;
    expect(el.errors.email).to.exist;
  });

  it('validates email format', async () => {
    const el = await fixture(html`<contact-form></contact-form>`);
    
    el.formData = { ...el.formData, email: 'invalid-email' };
    el.validateForm();
    
    expect(el.errors.email).to.include('non valida');
  });
});
```

#### Task 4.2.2: Integration tests (2 SP)

```javascript
// DELIVERABLE: tests/integration.test.js
describe('Integration Tests', () => {
  it('navigation scrolls to sections', async () => {
    // Mock scroll behavior
    let scrollTarget = null;
    Element.prototype.scrollIntoView = function(options) {
      scrollTarget = this.id;
    };

    const nav = await fixture(html`<app-navigation></app-navigation>`);
    const servicesLink = nav.shadowRoot.querySelector('[data-section="services"]');
    
    servicesLink.click();
    expect(scrollTarget).to.equal('services');
  });

  it('form submission triggers analytics', async () => {
    const form = await fixture(html`<contact-form></contact-form>`);
    
    let trackedEvent = null;
    form.trackEvent = (event, data) => {
      trackedEvent = { event, data };
    };

    form.formData = {
      name: 'Test User',
      email: 'test@example.com',
      challenge: 'Test challenge'
    };

    await form.handleSubmit(new Event('submit'));
    expect(trackedEvent.event).to.equal('form_submit_success');
  });
});
```

#### Task 4.2.3: Performance testing (1 SP)

```javascript
// DELIVERABLE: tests/performance.test.js
describe('Performance Tests', () => {
  it('loads critical resources quickly', async () => {
    const startTime = performance.now();
    
    // Load main app
    const app = await fixture(html`<tech-citizen-app></tech-citizen-app>`);
    
    const loadTime = performance.now() - startTime;
    expect(loadTime).to.be.below(1000); // Under 1 second
  });

  it('lazy loads non-critical components', async () => {
    const carousel = document.querySelector('tech-carousel');
    
    // Should not be loaded initially
    expect(carousel).to.be.null;
    
    // Simulate scroll to trigger loading
    window.dispatchEvent(new Event('scroll'));
    
    // Wait for lazy loading
    await new Promise(resolve => setTimeout(resolve, 100));
    
    const loadedCarousel = document.querySelector('tech-carousel');
    expect(loadedCarousel).to.exist;
  });
});
```

**Definition of Done**: All tests pass, coverage >80%, performance benchmarks met

---

## 📊 Definition of Done

### ✅ Component Level

- [ ] Component renders correctly in all breakpoints (mobile, tablet, desktop)
- [ ] All user interactions work as expected
- [ ] Accessibility requirements met (ARIA labels, keyboard navigation)
- [ ] Analytics tracking implemented for key events
- [ ] Error states handled gracefully
- [ ] Loading states implemented where needed
- [ ] Unit tests written and passing

### ✅ Feature Level  

- [ ] User story acceptance criteria met
- [ ] Integration tests pass
- [ ] Cross-browser compatibility verified (Chrome, Firefox, Safari)
- [ ] Performance benchmarks met (LCP < 2.5s, CLS < 0.1)
- [ ] SEO meta tags updated
- [ ] Documentation updated

### ✅ Sprint Level

- [ ] All user stories completed
- [ ] Code reviewed and approved
- [ ] Deployed to staging environment
- [ ] User acceptance testing completed
- [ ] Performance audit passed
- [ ] Security review completed

### ✅ Project Level

- [ ] Site live on tech-citizen.me
- [ ] DNS propagation verified
- [ ] HTTPS certificate valid
- [ ] Analytics tracking verified
- [ ] Contact form submissions working
- [ ] Performance optimized for production
- [ ] Monitoring and alerting configured

---

## 🧪 Testing Strategy

### Unit Testing (TDD Approach)

```javascript
// 1. Write failing test
describe('ContactForm validation', () => {
  it('should reject invalid email', () => {
    const form = new ContactForm();
    form.formData.email = 'invalid';
    expect(form.validateForm()).to.be.false;
  });
});

// 2. Write minimal code to pass
validateEmail(email) {
  return /\S+@\S+\.\S+/.test(email);
}

// 3. Refactor and improve
```

### Integration Testing

- **Component Communication**: Verify events flow correctly between components
- **Navigation**: Test smooth scrolling and section highlighting
- **Form Flow**: End-to-end form submission and validation
- **Analytics**: Verify tracking events fire correctly

### Performance Testing  

- **Core Web Vitals**: LCP, FID, CLS measurements
- **Network Conditions**: Test on slow 3G connections
- **Bundle Size**: Monitor JavaScript bundle size
- **Caching**: Verify service worker caching

### Accessibility Testing

- **Screen Reader**: Test with NVDA/JAWS
- **Keyboard Navigation**: Tab through all interactive elements
- **Color Contrast**: Verify WCAG 2.1 AA compliance
- **Focus Management**: Proper focus indicators

---

## 🔄 XP Practices Implementation

### Test-Driven Development (TDD)

1. **Red**: Write failing test
2. **Green**: Write minimal code to pass
3. **Refactor**: Improve code while keeping tests green

### Continuous Integration

```yaml
# .github/workflows/ci.yml
name: CI
on: [push, pull_request]
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - name: Install dependencies
        run: npm install
      - name: Run tests
        run: npm test
      - name: Build
        run: npm run build
      - name: Deploy to staging
        if: github.ref == 'refs/heads/main'
        run: npm run deploy:staging
```

### Pair Programming Guidelines

- **Driver/Navigator**: Rotate every 25 minutes
- **Code Review**: All code reviewed before merge
- **Knowledge Sharing**: Document architectural decisions

### Simple Design (YAGNI)

- Build only what's needed for current user stories
- Avoid over-engineering for future requirements
- Refactor when adding new features, not preemptively

### Collective Code Ownership

- Any developer can modify any code
- Consistent coding standards across project
- Shared responsibility for code quality

---

## 📈 Success Metrics

### Technical Metrics

- **Performance**: LCP < 2.5s, FID < 100ms, CLS < 0.1
- **Accessibility**: WCAG 2.1 AA compliance
- **SEO**: Lighthouse SEO score > 90
- **Test Coverage**: >80% unit test coverage

### Business Metrics  

- **Lead Generation**: Contact form submissions
- **Engagement**: Time on page, scroll depth
- **Conversion**: CTA click-through rates
- **Technical Credibility**: Technology section engagement

### Development Metrics

- **Velocity**: Story points completed per sprint
- **Quality**: Bugs found in production
- **Cycle Time**: Feature completion time
- **Team Satisfaction**: Retrospective feedback

---

## 🚀 Getting Started

### Prerequisites

```bash
# Modern browser with ES6 modules support
# Node.js 16+ (for development tools)
# Git for version control
```

### Quick Start

```bash
# 1. Clone/create project structure
mkdir tech-citizen-landing
cd tech-citizen-landing

# 2. Create basic files
touch index.html
mkdir -p js/{components,i18n/locales,data,utils}
mkdir -p css assets tests

# 3. Start with Sprint 1, Task 1.1.1
# Create index.html with basic structure

# 4. Follow task-by-task implementation
# Each task has clear deliverables and acceptance criteria
```

### Development Workflow

```bash
# 1. Pick next task from sprint backlog
# 2. Write failing test (if applicable)
# 3. Implement minimal solution
# 4. Run tests and verify
# 5. Refactor and improve
# 6. Commit with descriptive message
# 7. Move to next task
```

---

**Ready to build enterprise-grade landing page with XP practices! 🎯**

Each task is atomic, testable, and follows SOLID principles. Perfect for step-by-step implementation with Copilot assistance.
