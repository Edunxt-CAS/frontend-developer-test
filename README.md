# EduNXT Frontend Developer Coding Test
## React Table Components & Laravel Blade Conversion

### Overview
This coding test evaluates a frontend developer's ability to create reusable React components, work with APIs, and convert existing templates to React. The test consists of 3 progressive tasks that build upon each other.

**Time Allocation: 6-8 hours total**
- Task 1: 2 hours
- Task 2: 2 hours  
- Task 3: 1-2 hours
- Task 4: 2-3 hours

---

## Task 1: Basic Reusable Table Component (2 hours)

### Objective
Create a reusable React table component that can display data from any API with basic functionality.

### Requirements

#### Core Features
1. **Reusable Table Component** (`DataTable.jsx`)
   - Accept data via props
   - Dynamic column configuration
   - Responsive design
   - Loading and error states
   - Empty state handling

2. **Column Configuration**
   ```javascript
   const columns = [
     { key: 'id', label: 'ID', sortable: true },
     { key: 'name', label: 'Name', sortable: true },
     { key: 'email', label: 'Email', sortable: false },
     { key: 'actions', label: 'Actions', render: (row) => <ActionButtons row={row} /> }
   ];
   ```

3. **Basic Sorting**
   - Click column headers to sort
   - Visual indicators for sort direction
   - Support for string and numeric sorting

#### API Integration
Use the following dummy API endpoints:

**Users API:**
```
GET https://jsonplaceholder.typicode.com/users
```

**Posts API:**
```
GET https://jsonplaceholder.typicode.com/posts
```

#### Technical Requirements
- Use React functional components with hooks
- Implement proper TypeScript types (optional but preferred)
- Use CSS modules or styled-components for styling
- Handle async operations properly
- Include error boundaries

#### Deliverables
1. `DataTable.jsx` - Main table component
2. `UsersList.jsx` - Users table implementation
3. `PostsList.jsx` - Posts table implementation
4. Basic styling (CSS/SCSS files)
5. README with usage instructions

### Evaluation Criteria
- **Code Quality** (25%): Clean, readable, maintainable code
- **Reusability** (25%): Component can be easily reused with different data
- **Functionality** (25%): All basic features work correctly
- **Error Handling** (25%): Proper loading states and error handling

---

## Task 2: Advanced Table with Additional Features (2 hours)

### Objective
Enhance the basic table component with advanced features like column visibility, export functionality, and filtering.

### Requirements

#### Enhanced Features
1. **Column Visibility Toggle**
   - Dropdown/modal to show/hide columns
   - Remember user preferences (localStorage)
   - Minimum one column must remain visible

2. **Export Functionality**
   - Export to CSV format
   - Export to JSON format
   - Export visible data only or all data
   - Custom filename generation

3. **Global Search/Filter**
   - Search across all visible columns
   - Real-time filtering as user types
   - Highlight matching text (bonus)

4. **Pagination**
   - Client-side pagination
   - Configurable page sizes (10, 25, 50, 100)
   - Page navigation controls

#### Additional API Integration
Use this enhanced dummy API:

**Products API:**
```
GET https://dummyjson.com/products
```

**Comments API:**
```
GET https://dummyjson.com/comments
```

#### Enhanced Column Configuration
```javascript
const columns = [
  { 
    key: 'id', 
    label: 'ID', 
    sortable: true, 
    filterable: true,
    exportable: true,
    visible: true 
  },
  { 
    key: 'title', 
    label: 'Title', 
    sortable: true, 
    filterable: true,
    exportable: true,
    visible: true,
    width: 200 
  },
  { 
    key: 'price', 
    label: 'Price', 
    sortable: true, 
    filterable: false,
    exportable: true,
    visible: true,
    format: (value) => `$${value}`,
    type: 'number'
  }
];
```

#### Technical Requirements
- Extend the existing table component
- Implement proper state management
- Add loading indicators for exports
- Use modern JavaScript features (ES6+)
- Responsive design for mobile devices

#### Deliverables
1. Enhanced `DataTable.jsx` with new features
2. `ColumnVisibilityToggle.jsx` component
3. `ExportButton.jsx` component
4. `SearchFilter.jsx` component
5. `Pagination.jsx` component
6. `ProductsTable.jsx` - Products table implementation
7. Updated styling
8. Updated README with new features

### Evaluation Criteria
- **Feature Implementation** (30%): All advanced features work correctly
- **User Experience** (25%): Intuitive interface and smooth interactions
- **Code Architecture** (25%): Well-structured, modular code
- **Performance** (20%): Efficient handling of large datasets

---

## Task 3: Laravel Blade to React Conversion (1-2 hours)

### Objective
Convert a Laravel Blade template to a React component, maintaining the same functionality and styling.

### Laravel Blade Template to Convert

```php
{{-- resources/views/dashboard/analytics.blade.php --}}
@extends('layouts.app')

@section('title', 'Analytics Dashboard')

@section('content')
<div class="analytics-dashboard">
    <div class="dashboard-header">
        <h1>Analytics Overview</h1>
        <div class="date-range-picker">
            <select name="period" id="period">
                <option value="7">Last 7 days</option>
                <option value="30">Last 30 days</option>
                <option value="90">Last 90 days</option>
            </select>
        </div>
    </div>

    <div class="stats-grid">
        @foreach($stats as $stat)
            <div class="stat-card {{ $stat['trend'] }}">
                <div class="stat-icon">
                    <i class="fas fa-{{ $stat['icon'] }}"></i>
                </div>
                <div class="stat-content">
                    <h3>{{ $stat['title'] }}</h3>
                    <p class="stat-value">{{ number_format($stat['value']) }}</p>
                    <span class="stat-change">
                        {{ $stat['change'] }}% from last period
                    </span>
                </div>
            </div>
        @endforeach
    </div>

    <div class="charts-section">
        <div class="chart-container">
            <h2>Revenue Trend</h2>
            <canvas id="revenueChart"></canvas>
        </div>
        <div class="chart-container">
            <h2>User Growth</h2>
            <canvas id="userChart"></canvas>
        </div>
    </div>

    <div class="recent-activity">
        <h2>Recent Activity</h2>
        <div class="activity-list">
            @forelse($activities as $activity)
                <div class="activity-item">
                    <div class="activity-avatar">
                        <img src="{{ $activity->user->avatar }}" alt="{{ $activity->user->name }}">
                    </div>
                    <div class="activity-content">
                        <p><strong>{{ $activity->user->name }}</strong> {{ $activity->description }}</p>
                        <span class="activity-time">{{ $activity->created_at->diffForHumans() }}</span>
                    </div>
                </div>
            @empty
                <p class="no-activity">No recent activity</p>
            @endforelse
        </div>
    </div>
</div>
@endsection

@push('scripts')
<script>
    // Chart initialization code
    const revenueChart = new Chart(document.getElementById('revenueChart'), {
        type: 'line',
        data: {!! json_encode($chartData) !!},
        options: {
            responsive: true,
            scales: {
                y: {
                    beginAtZero: true
                }
            }
        }
    });
</script>
@endpush
```

### Associated CSS (SCSS)
```scss
.analytics-dashboard {
    padding: 20px;
    
    .dashboard-header {
        display: flex;
        justify-content: space-between;
        align-items: center;
        margin-bottom: 30px;
        
        h1 {
            color: #333;
            font-size: 2rem;
        }
        
        .date-range-picker select {
            padding: 8px 12px;
            border: 1px solid #ddd;
            border-radius: 4px;
        }
    }
    
    .stats-grid {
        display: grid;
        grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
        gap: 20px;
        margin-bottom: 30px;
        
        .stat-card {
            background: white;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 2px 4px rgba(0,0,0,0.1);
            display: flex;
            align-items: center;
            
            &.positive {
                border-left: 4px solid #10b981;
            }
            
            &.negative {
                border-left: 4px solid #ef4444;
            }
            
            .stat-icon {
                font-size: 2rem;
                color: #6b7280;
                margin-right: 15px;
            }
            
            .stat-content {
                h3 {
                    margin: 0 0 5px 0;
                    color: #6b7280;
                    font-size: 0.9rem;
                }
                
                .stat-value {
                    font-size: 1.8rem;
                    font-weight: bold;
                    color: #111827;
                    margin: 0;
                }
                
                .stat-change {
                    font-size: 0.8rem;
                    color: #6b7280;
                }
            }
        }
    }
    
    .charts-section {
        display: grid;
        grid-template-columns: 1fr 1fr;
        gap: 20px;
        margin-bottom: 30px;
        
        .chart-container {
            background: white;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 2px 4px rgba(0,0,0,0.1);
            
            h2 {
                margin-top: 0;
                color: #333;
            }
        }
    }
    
    .recent-activity {
        background: white;
        padding: 20px;
        border-radius: 8px;
        box-shadow: 0 2px 4px rgba(0,0,0,0.1);
        
        .activity-list {
            .activity-item {
                display: flex;
                align-items: center;
                padding: 15px 0;
                border-bottom: 1px solid #f3f4f6;
                
                &:last-child {
                    border-bottom: none;
                }
                
                .activity-avatar img {
                    width: 40px;
                    height: 40px;
                    border-radius: 50%;
                    margin-right: 15px;
                }
                
                .activity-content {
                    p {
                        margin: 0 0 5px 0;
                        color: #333;
                    }
                    
                    .activity-time {
                        color: #6b7280;
                        font-size: 0.8rem;
                    }
                }
            }
            
            .no-activity {
                text-align: center;
                color: #6b7280;
                padding: 20px;
            }
        }
    }
}

@media (max-width: 768px) {
    .analytics-dashboard {
        .charts-section {
            grid-template-columns: 1fr;
        }
        
        .dashboard-header {
            flex-direction: column;
            gap: 15px;
            align-items: flex-start;
        }
    }
}
```

### Requirements

#### Conversion Tasks
1. **Convert Blade Template to React Component**
   - Create `AnalyticsDashboard.jsx` component
   - Maintain the same visual layout and styling
   - Convert PHP loops to JavaScript map functions
   - Handle conditional rendering appropriately

2. **Create Mock Data Structure**
   - Define mock data that matches the Laravel structure
   - Create dummy API endpoints or static data
   - Include realistic sample data

3. **Implement Interactive Features**
   - Working date range picker
   - Chart placeholders (use Chart.js or similar)
   - Responsive design maintained

#### Mock Data APIs
Create mock data for:

**Stats API:**
```json
{
  "stats": [
    {
      "title": "Total Revenue",
      "value": 45678,
      "change": 12.5,
      "trend": "positive",
      "icon": "dollar-sign"
    },
    {
      "title": "Active Users",
      "value": 1234,
      "change": -2.3,
      "trend": "negative", 
      "icon": "users"
    }
  ]
}
```

**Activities API:**
```json
{
  "activities": [
    {
      "id": 1,
      "user": {
        "name": "John Doe",
        "avatar": "https://via.placeholder.com/40"
      },
      "description": "completed a purchase",
      "created_at": "2024-01-15T10:30:00Z"
    }
  ]
}
```

#### Technical Requirements
- Use React functional components
- Implement proper state management
- Convert SCSS to CSS modules or styled-components
- Maintain responsive design
- Add proper loading states

#### Deliverables
1. `AnalyticsDashboard.jsx` - Main dashboard component
2. `StatCard.jsx` - Individual stat card component
3. `ActivityItem.jsx` - Activity list item component
4. `DateRangePicker.jsx` - Date range selector
5. Mock data files or API integration
6. Converted CSS/styling
7. Documentation explaining conversion decisions

### Evaluation Criteria
- **Accuracy** (30%): How closely the React version matches the original
- **Code Quality** (25%): Clean, maintainable React code
- **Functionality** (25%): Interactive features work correctly
- **Styling** (20%): Visual consistency and responsiveness maintained

## Task 4: Beautiful Modern Dashboard Creation (2-3 hours)

### Objective
Create a visually stunning, modern dashboard with advanced UI/UX features, animations, and interactive data visualizations. This task focuses on design aesthetics, user experience, and modern web development techniques.

### Requirements

#### Dashboard Theme Options (Choose One)
1. **Executive Business Dashboard**
   - Sales analytics and KPIs
   - Revenue tracking and forecasting
   - Team performance metrics

2. **E-commerce Analytics Dashboard**
   - Product performance and inventory
   - Customer behavior analysis
   - Order and revenue tracking

3. **Social Media Management Dashboard**
   - Engagement metrics and analytics
   - Content performance tracking
   - Audience demographics

#### Core Design Requirements

##### 1. Modern Visual Design
- **Color Scheme**: Choose a cohesive, modern color palette
  - Primary, secondary, and accent colors
  - Dark mode support (bonus)
  - Proper contrast ratios for accessibility

- **Typography**: Modern font hierarchy
  - Use Google Fonts or system fonts
  - Consistent font sizes and weights
  - Proper line spacing and readability

- **Layout**: Contemporary grid system
  - Card-based design with proper spacing
  - Consistent border radius and shadows
  - Responsive breakpoints

##### 2. Advanced Visual Components
- **Interactive Charts** (Choose 2-3 types):
  ```javascript
  // Example chart configurations
  const charts = [
    {
      type: 'area',
      title: 'Revenue Trend',
      data: monthlyRevenue,
      gradient: true,
      interactive: true
    },
    {
      type: 'donut',
      title: 'Traffic Sources',
      data: trafficSources,
      animations: true,
      tooltips: true
    },
    {
      type: 'bar',
      title: 'Product Performance',
      data: productSales,
      horizontal: true,
      colorScale: true
    }
  ];
  ```

- **KPI Cards with Animations**:
  ```javascript
  const kpis = [
    {
      title: 'Total Revenue',
      value: 125400,
      change: '+12.5%',
      trend: 'up',
      icon: 'trending-up',
      color: 'success',
      sparkline: [65, 59, 80, 81, 56, 55, 40]
    },
    {
      title: 'Active Users',
      value: 8465,
      change: '-2.3%',
      trend: 'down',
      icon: 'users',
      color: 'warning',
      sparkline: [28, 48, 40, 19, 86, 27, 90]
    }
  ];
  ```

##### 3. Interactive Elements
- **Animated Counters**: Numbers count up on component mount
- **Hover Effects**: Smooth transitions and micro-interactions
- **Loading Skeletons**: Beautiful loading states
- **Interactive Filters**: 
  - Date range picker with presets
  - Multi-select dropdown filters
  - Search functionality with debouncing

##### 4. Modern UI Patterns
- **Glassmorphism Effects**: Translucent cards with backdrop blur
- **Neumorphism Elements**: Soft shadows and highlights (optional)
- **Gradient Backgrounds**: Dynamic gradient overlays
- **Floating Action Buttons**: Context-aware actions
- **Toast Notifications**: Success/error feedback

#### Technical Implementation

##### Component Architecture
```javascript
// Suggested component structure
src/
├── components/
│   ├── Dashboard/
│   │   ├── DashboardLayout.jsx
│   │   ├── Sidebar.jsx
│   │   ├── TopBar.jsx
│   │   └── MainContent.jsx
│   ├── Charts/
│   │   ├── AreaChart.jsx
│   │   ├── DonutChart.jsx
│   │   ├── BarChart.jsx
│   │   └── SparklineChart.jsx
│   ├── Cards/
│   │   ├── KPICard.jsx
│   │   ├── StatCard.jsx
│   │   └── MetricCard.jsx
│   ├── Filters/
│   │   ├── DateRangePicker.jsx
│   │   ├── FilterDropdown.jsx
│   │   └── SearchBar.jsx
│   └── UI/
│       ├── Button.jsx
│       ├── Card.jsx
│       ├── LoadingSkeleton.jsx
│       └── AnimatedCounter.jsx
```

##### Animation Requirements
```javascript
// Example animation implementations
const cardVariants = {
  hidden: { opacity: 0, y: 20 },
  visible: { 
    opacity: 1, 
    y: 0,
    transition: { duration: 0.6, ease: "easeOut" }
  }
};

const counterAnimation = {
  from: 0,
  to: targetValue,
  duration: 2000,
  easing: 'easeOutQuart'
};
```

#### Mock Data APIs

##### Dashboard Analytics API
```json
{
  "overview": {
    "totalRevenue": 125400,
    "revenueChange": 12.5,
    "totalUsers": 8465,
    "usersChange": -2.3,
    "conversionRate": 3.2,
    "conversionChange": 0.8,
    "averageOrderValue": 89.50,
    "aovChange": 5.2
  },
  "charts": {
    "revenueByMonth": [
      { "month": "Jan", "revenue": 4200, "users": 1200 },
      { "month": "Feb", "revenue": 5100, "users": 1350 },
      { "month": "Mar", "revenue": 6200, "users": 1500 }
    ],
    "trafficSources": [
      { "source": "Organic Search", "value": 45, "color": "#10b981" },
      { "source": "Social Media", "value": 25, "color": "#3b82f6" },
      { "source": "Direct", "value": 20, "color": "#f59e0b" },
      { "source": "Referral", "value": 10, "color": "#ef4444" }
    ],
    "topProducts": [
      { "name": "Premium Plan", "sales": 1250, "revenue": 25000 },
      { "name": "Basic Plan", "sales": 850, "revenue": 12750 },
      { "name": "Enterprise Plan", "sales": 320, "revenue": 16000 }
    ]
  },
  "recentActivity": [
    {
      "id": 1,
      "type": "sale",
      "message": "New order #12345 received",
      "value": "$250.00",
      "timestamp": "2024-06-18T10:30:00Z",
      "status": "success"
    },
    {
      "id": 2,
      "type": "user",
      "message": "New user registration",
      "value": "john.doe@email.com",
      "timestamp": "2024-06-18T09:15:00Z",
      "status": "info"
    }
  ]
}
```

##### Real-time Updates Simulation
```javascript
// Simulate real-time data updates
const useRealTimeData = () => {
  const [data, setData] = useState(initialData);
  
  useEffect(() => {
    const interval = setInterval(() => {
      setData(prevData => ({
        ...prevData,
        overview: {
          ...prevData.overview,
          totalRevenue: prevData.overview.totalRevenue + Math.random() * 100,
          totalUsers: prevData.overview.totalUsers + Math.floor(Math.random() * 5)
        }
      }));
    }, 5000);
    
    return () => clearInterval(interval);
  }, []);
  
  return data;
};
```

#### Advanced Features

##### 1. Theme Customization
```javascript
const themes = {
  light: {
    primary: '#3b82f6',
    secondary: '#64748b',
    background: '#f8fafc',
    surface: '#ffffff',
    text: '#1e293b'
  },
  dark: {
    primary: '#60a5fa',
    secondary: '#94a3b8',
    background: '#0f172a',
    surface: '#1e293b',
    text: '#f1f5f9'
  },
  corporate: {
    primary: '#059669',
    secondary: '#6b7280',
    background: '#f9fafb',
    surface: '#ffffff',
    text: '#111827'
  }
};
```

##### 2. Performance Optimization
- Implement virtualization for large data sets
- Lazy loading for charts and heavy components
- Memoization for expensive calculations
- Debounced search and filter inputs

##### 3. Accessibility Features
- Keyboard navigation support
- Screen reader friendly
- Focus management
- Color blind friendly palettes
- Proper ARIA labels

##### 4. Responsive Design Breakpoints
```css
/* Mobile First Approach */
.dashboard-grid {
  display: grid;
  gap: 1rem;
  grid-template-columns: 1fr;
  
  @media (min-width: 768px) {
    grid-template-columns: repeat(2, 1fr);
  }
  
  @media (min-width: 1024px) {
    grid-template-columns: repeat(3, 1fr);
  }
  
  @media (min-width: 1280px) {
    grid-template-columns: repeat(4, 1fr);
  }
}
```

#### Design Inspiration Sources
- **Dribbble**: Search for "dashboard UI" or "analytics dashboard"
- **Behance**: Modern dashboard designs
- **UI8**: Dashboard templates and components
- **Tailwind UI**: Professional dashboard examples

#### Recommended Libraries

##### Charting Libraries
- **Recharts**: React-specific charting library
- **Chart.js with react-chartjs-2**: Powerful and flexible
- **D3.js**: For custom, advanced visualizations
- **Victory**: Modular charting components

##### Animation Libraries
- **Framer Motion**: Production-ready motion library
- **React Spring**: Spring-physics based animations
- **Lottie React**: After Effects animations
- **React Transition Group**: Transition components

##### UI Enhancement Libraries
- **React Hot Toast**: Beautiful notifications
- **React Date Range**: Advanced date pickers
- **React Select**: Enhanced select components
- **React Virtualized**: Performance for large lists

#### Deliverables
1. **Complete Dashboard Application**
   - Fully functional React dashboard
   - Multiple chart types with real data
   - Interactive filters and controls
   - Responsive design

2. **Component Library**
   - Reusable chart components
   - Custom KPI cards
   - Filter components
   - UI components (buttons, cards, etc.)

3. **Styling System**
   - Consistent design tokens
   - Theme configuration
   - Responsive utilities
   - Animation definitions

4. **Documentation**
   - Component usage guide
   - Theme customization guide
   - Performance optimization notes
   - Accessibility features documentation

5. **Design Assets**
   - Color palette documentation
   - Typography scale
   - Component variations
   - Responsive breakpoint guide

### Evaluation Criteria

#### Visual Design (30%)
- **Aesthetic Appeal**: Modern, professional appearance
- **Consistency**: Cohesive design language throughout
- **Color Usage**: Effective color scheme and contrast
- **Typography**: Proper font hierarchy and readability

#### User Experience (25%)
- **Interactivity**: Smooth animations and transitions
- **Responsiveness**: Works well on all device sizes
- **Accessibility**: Keyboard navigation and screen reader support
- **Performance**: Fast loading and smooth interactions

#### Technical Implementation (25%)
- **Code Quality**: Clean, maintainable React code
- **Component Architecture**: Well-structured and reusable components
- **State Management**: Proper handling of complex state
- **Performance**: Optimized for large datasets

#### Innovation & Creativity (20%)
- **Unique Features**: Creative solutions and features
- **Advanced Techniques**: Use of modern web technologies
- **Attention to Detail**: Polished micro-interactions
- **Problem Solving**: Creative solutions to UX challenges

### Bonus Features
- **Real-time Data Updates**: WebSocket integration simulation
- **Export Functionality**: Dashboard export to PDF/PNG
- **Drag & Drop**: Customizable dashboard layout
- **Progressive Web App**: PWA features for mobile
- **Data Visualization**: Custom D3.js visualizations
- **Advanced Filters**: Complex filter combinations
- **Collaborative Features**: Share dashboard views
- **Performance Monitoring**: Component performance metrics

---

## Submission Guidelines

### What to Submit
1. **Source Code**
   - All React components
   - Styling files (CSS/SCSS/styled-components)
   - Package.json with dependencies
   - Any mock data files

2. **Documentation**
   - README.md with setup instructions
   - Component usage examples
   - API integration details
   - Any assumptions or design decisions

3. **Demo**
   - Working application (deployed or local)
   - Screenshots of key features
   - Screen recording of functionality (optional)

### Setup Instructions
Include clear instructions for:
- Node.js and npm/yarn requirements
- Installation steps
- How to run the development server
- How to build for production

### Code Quality Standards
- Use consistent formatting (Prettier recommended)
- Include appropriate comments
- Follow React best practices
- Handle edge cases and errors
- Write semantic, accessible HTML

### Bonus Points
- TypeScript implementation
- Unit tests using Jest/React Testing Library
- Mobile-first responsive design
- Performance optimizations
- Accessibility features (ARIA labels, keyboard navigation)
- Clean Git history with meaningful commits

---

## Evaluation Matrix

| Criteria | Task 1 Weight | Task 2 Weight | Task 3 Weight | Task 4 Weight | Total Weight |
|----------|---------------|---------------|---------------|---------------|--------------|
| **Functionality** | 25% | 30% | 25% | 20% | 25% |
| **Code Quality** | 25% | 25% | 25% | 25% | 25% |
| **User Experience** | 20% | 25% | 20% | 35% | 25% |
| **Technical Implementation** | 30% | 20% | 30% | 20% | 25% |

### Scoring Scale
- **Excellent (90-100%)**: Exceeds expectations, production-ready code
- **Good (80-89%)**: Meets all requirements with minor issues
- **Satisfactory (70-79%)**: Meets most requirements, some missing features
- **Needs Improvement (60-69%)**: Basic functionality, significant issues
- **Unsatisfactory (<60%)**: Major functionality missing or broken

---

## Additional Resources

### Recommended Libraries
- **React**: ^18.0.0
- **React Router**: For navigation (if needed)
- **Axios**: For API calls
- **Chart.js/Recharts**: For charts
- **Date-fns/Moment.js**: For date handling
- **Lodash**: For utility functions

### Helpful APIs
- JSONPlaceholder: https://jsonplaceholder.typicode.com/
- DummyJSON: https://dummyjson.com/
- Fake Store API: https://fakestoreapi.com/

### Design Resources
- Tailwind CSS: https://tailwindcss.com/
- Material-UI: https://mui.com/
- Ant Design: https://ant.design/
- Font Awesome: https://fontawesome.com/

---

## FAQ

**Q: Can I use a UI library like Material-UI or Ant Design?**
A: Yes, but prioritize demonstrating your ability to create custom components.

**Q: What if I don't finish all tasks?**
A: Submit what you have completed. Partial completion with good quality is better than rushed, incomplete work.

**Q: Can I use TypeScript?**
A: Yes, TypeScript is encouraged and will earn bonus points.

**Q: How should I handle the chart functionality in Task 3?**
A: You can use placeholder charts or integrate a simple charting library. Focus on the component structure and data flow.

**Q: What browser support is required?**
A: Modern browsers (Chrome, Firefox, Safari, Edge) - no IE support needed.

---

*Good luck! We're excited to see your React development skills in action.*
