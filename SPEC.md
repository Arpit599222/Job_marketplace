# AI Job & Internship Marketplace - Specification

## 1. Concept & Vision

A sleek, professional job marketplace platform that helps users discover opportunities based on their skills. The platform emphasizes real job/internship listings with AI-powered match analysis as a supporting feature. The experience should feel like a polished recruitment platform where AI adds value without being the core product.

## 2. Design Language

### Aesthetic Direction
Modern recruitment platform inspired by LinkedIn and Indeed, but cleaner and more focused. Professional yet approachable, with clear visual hierarchy and trust-building design patterns.

### Color Palette
- **Primary**: `#4F46E5` (Indigo-600) - Main actions, branding
- **Primary Light**: `#818CF8` (Indigo-400) - Hover states
- **Success**: `#10B981` (Emerald-500) - High match indicators
- **Warning**: `#F59E0B` (Amber-500) - Medium match indicators
- **Danger**: `#EF4444` (Red-500) - Low match indicators
- **Background**: `#F9FAFB` (Gray-50) - Page background
- **Card Background**: `#FFFFFF` - Card surfaces
- **Text Primary**: `#111827` (Gray-900) - Headlines
- **Text Secondary**: `#6B7280` (Gray-500) - Body text
- **Border**: `#E5E7EB` (Gray-200) - Subtle borders

### Typography
- **Font Family**: Inter (Google Fonts) with system fallbacks
- **Headings**: Inter, 700 weight
  - H1: 2.25rem (36px)
  - H2: 1.5rem (24px)
  - H3: 1.125rem (18px)
- **Body**: Inter, 400 weight, 1rem (16px)
- **Small**: 0.875rem (14px)

### Spatial System
- Base unit: 4px
- Card padding: 24px (6 units)
- Section spacing: 32px (8 units)
- Grid gap: 24px (6 units)
- Border radius: 12px (cards), 8px (buttons), 6px (inputs)

### Motion Philosophy
- **Page transitions**: None (single page app)
- **Component reveals**: Fade in, 200ms ease-out
- **Hover effects**: Scale(1.02) on cards, color shift on buttons, 150ms
- **Modal animations**: Fade in + scale from 0.95 to 1, 200ms ease-out
- **Loading states**: Pulse animation on skeleton loaders

### Visual Assets
- **Icons**: Heroicons (outline style)
- **Decorative**: Minimal - focus on content
- **Shadows**: Soft, multi-layered shadows for depth
  - Cards: `0 1px 3px rgba(0,0,0,0.1), 0 1px 2px rgba(0,0,0,0.06)`
  - Elevated: `0 10px 15px -3px rgba(0,0,0,0.1), 0 4px 6px -2px rgba(0,0,0,0.05)`
  - Modal: `0 25px 50px -12px rgba(0,0,0,0.25)`

## 3. Layout & Structure

### Page Structure
```
┌─────────────────────────────────────────────┐
│  Header (Hero Section)                      │
│  - Title, Subtitle, Visual accent           │
├─────────────────────────────────────────────┤
│  User Input Panel (Sidebar/Top)             │
│  - Skills input                             │
│  - Experience dropdown                       │
│  - Projects textarea                         │
│  - Find Opportunities button                │
├─────────────────────────────────────────────┤
│  Filter Bar                                 │
│  - Search input                             │
│  - Type filter (All/Jobs/Internships)      │
├─────────────────────────────────────────────┤
│  Marketplace Grid (Main Content)            │
│  ┌──────────┐ ┌──────────┐ ┌──────────┐      │
│  │ Job Card│ │Job Card │ │Job Card │       │
│  │  72%    │ │  85%    │ │  45%    │       │
│  └──────────┘ └──────────┘ └──────────┘      │
│  ┌──────────┐ ┌──────────┐ ┌──────────┐      │
│  │Job Card │ │Job Card │ │Job Card │       │
│  └──────────┘ └──────────┘ └──────────┘      │
├─────────────────────────────────────────────┤
│  Match Modal (Overlay)                      │
│  - Match percentage (large)                 │
│  - Matched skills (green)                   │
│  - Missing skills (red)                     │
│  - AI suggestion                            │
└─────────────────────────────────────────────┘
```

### Responsive Strategy
- **Desktop (1024px+)**: 3-column grid, sidebar input panel
- **Tablet (768px-1023px)**: 2-column grid, stacked input panel
- **Mobile (<768px)**: Single column, collapsible input panel

## 4. Features & Interactions

### User Input Panel
- **Skills Input**:
  - Text input with comma separation
  - Placeholder: "e.g., JavaScript, React, Node.js"
  - Validation: At least 1 skill required
- **Experience Dropdown**:
  - Options: Fresher, 1 year, 2+ years
  - Default: Fresher
- **Projects Textarea**:
  - Optional, multiline
  - Placeholder: "Describe your projects..."
  - Min height: 100px
- **Find Opportunities Button**:
  - Primary indigo color
  - Disabled state when skills empty
  - Loading state while fetching

### Search & Filter Bar
- **Search Input**:
  - Filters by job title or skills
  - Real-time filtering (debounced 300ms)
  - Clear button when text present
- **Filter Buttons**:
  - "All" (default selected)
  - "Jobs 💼"
  - "Internships 🎓"
  - Pill-style toggle buttons
  - Active state with primary color

### Job/Internship Cards
- **States**: Default, Hover, Loading
- **Elements**:
  - Type badge (Job/Internship) with icon
  - Job title (prominent)
  - Company name (optional)
  - Required skills as tags
  - Location (if available)
  - Salary range (if available)
  - "Check Match" button
- **Interactions**:
  - Hover lifts card with shadow increase
  - Click "Check Match" opens modal with AI analysis

### AI Match Modal
- **Trigger**: Click "Check Match" button on any job card
- **Loading State**: Skeleton loader while AI analyzes
- **Content**:
  - Large match percentage (centered, color-coded)
  - Matched skills list (green checkmarks)
  - Missing skills list (red X marks)
  - AI suggestion paragraph
  - Close button
- **Animation**: Fade in + scale up from center
- **Backdrop**: Semi-transparent dark overlay, click to close

## 5. Component Inventory

### Header Component
- **States**: Default
- **Elements**: Title (H1), Subtitle (p), decorative gradient accent
- **Styling**: Centered text, subtle gradient background

### UserInputForm Component
- **States**: Default, Validation error, Submitting
- **Elements**: SkillsInput, ExperienceSelect, ProjectsTextarea, SubmitButton
- **Validation**: Skills required, minimum 1 skill

### FilterBar Component
- **States**: Default
- **Elements**: SearchInput, FilterButtonGroup
- **Interactions**: Real-time filtering, button state management

### JobCard Component
- **States**: Default, Hover, Loading (when checking match)
- **Elements**: TypeBadge, Title, Company, SkillsList, MatchButton
- **Props**: job object, onCheckMatch callback

### MatchModal Component
- **States**: Hidden, Loading, Visible, Error
- **Elements**: Backdrop, ModalContainer, MatchPercentage, MatchedSkills, MissingSkills, Suggestion, CloseButton
- **Animations**: Fade in, scale from 0.95

### LoadingSpinner Component
- **States**: Active
- **Elements**: Animated spinner with text

## 6. Technical Approach

### Frontend Stack
- **Framework**: React 18 with Vite
- **Styling**: Tailwind CSS (utility-first)
- **Icons**: Heroicons (via @heroicons/react)
- **State Management**: React useState/useEffect (no external library)
- **Build Tool**: Vite

### Project Structure
```
src/
├── components/
│   ├── Header.jsx
│   ├── UserInputForm.jsx
│   ├── FilterBar.jsx
│   ├── JobCard.jsx
│   ├── MatchModal.jsx
│   └── LoadingSpinner.jsx
├── data/
│   └── mockJobs.js          # Sample job/internship data
├── utils/
│   └── aiMatching.js        # AI API integration
├── App.jsx
├── main.jsx
└── index.css                 # Tailwind + custom styles
```

### Mock Job Data Structure
```javascript
const mockJobs = [
  {
    id: 1,
    type: "job", // or "internship"
    title: "Frontend Developer",
    company: "TechCorp Solutions",
    location: "Remote",
    salary: "$80,000 - $100,000",
    skills: ["JavaScript", "React", "HTML", "CSS", "Git"],
    description: "Build modern web applications..."
  },
  // ... 12-15 more jobs
];
```

### AI Matching Integration (MiniMax)
```javascript
async function checkJobMatch(userProfile, job) {
  const prompt = `You are an AI assistant for a job marketplace.
Analyze how well the user matches this opportunity.

Return ONLY valid JSON:
{
  match_percentage: number (0-100),
  matched_skills: array of strings,
  missing_skills: array of strings,
  suggestion: string (short advice)
}

User Skills: ${userProfile.skills}
Experience: ${userProfile.experience}
Projects: ${userProfile.projects}
Job Requirements: ${job.skills.join(', ')}`;

  // API call to MiniMax
  // Return structured match data
}
```

### Job Matching Algorithm (Fallback)
```javascript
function calculateMatch(userSkills, jobSkills) {
  const userSkillSet = new Set(userSkills.map(s => s.toLowerCase()));
  const jobSkillSet = jobSkills.map(s => s.toLowerCase());
  
  const matched = jobSkillSet.filter(skill => userSkillSet.has(skill));
  const missing = jobSkillSet.filter(skill => !userSkillSet.has(skill));
  const percentage = Math.round((matched.length / jobSkillSet.length) * 100);
  
  return { percentage, matched, missing };
}
```

### State Management
```javascript
// Main App state
const [userProfile, setUserProfile] = useState({ skills: '', experience: 'Fresher', projects: '' });
const [jobs, setJobs] = useState(mockJobs);
const [filteredJobs, setFilteredJobs] = useState(mockJobs);
const [searchTerm, setSearchTerm] = useState('');
const [typeFilter, setTypeFilter] = useState('all');
const [selectedJob, setSelectedJob] = useState(null);
const [matchResult, setMatchResult] = useState(null);
const [isModalOpen, setIsModalOpen] = useState(false);
```

### Error Handling
- Empty skills input: Show validation message
- API failure: Use fallback algorithm, show error toast
- No search results: Show "No opportunities found" message
- Modal close: Click backdrop or X button

## 7. Mock Data Requirements

Generate 12-15 diverse job/internship listings:
- Frontend, Backend, Full Stack positions
- Web development, Mobile development
- Data Science, Machine Learning
- UI/UX Design
- DevOps, Cloud positions
- Mix of jobs (8-10) and internships (4-5)
- Varied skill requirements (2-6 skills per listing)
- Realistic company names and salary ranges
