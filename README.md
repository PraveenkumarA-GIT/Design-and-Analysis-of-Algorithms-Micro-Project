# 🚌 Transport Tracker MVP

**Real-Time Public Transport Tracking for Small Cities**

A lightweight, low-bandwidth optimized web application that provides real-time bus tracking for small cities and tier-2 towns. Built specifically to address the problem of unpredictable public transport schedules in areas with limited digital infrastructure.

![Transport Tracker](https://img.shields.io/badge/status-MVP-green) ![Node.js](https://img.shields.io/badge/node.js-v16+-blue) ![License](https://img.shields.io/badge/license-MIT-green)

## 🎯 Problem Statement

**Problem ID:** 25013  
**Title:** Real-Time Public Transport Tracking for Small Cities

In small cities and tier-2 towns, public transport systems lack real-time tracking, causing inconvenience to commuters who face unpredictable bus schedules. Over 60% of commuters face delays due to lack of real-time information, reducing public transport usage and increasing private vehicle dependency.

## ✨ Features

### Core Features
- 📍 **Real-time GPS tracking** of buses with live location updates
- ⏰ **Estimated arrival times** for all bus stops
- 🚌 **Route management** with multiple bus routes support
- 📊 **Bus occupancy levels** (low/medium/high indicators)
- 📱 **Mobile-responsive design** optimized for all devices
- 🌐 **Low-bandwidth optimization** for areas with limited internet

### Technical Features
- 🔄 **Auto-refresh** every 30 seconds for real-time updates
- 🎯 **RESTful API** with comprehensive endpoints
- 📡 **GPS simulation system** for testing and development
- 💾 **Lightweight architecture** (< 50KB total)
- 🔌 **Offline detection** and graceful degradation

## 🏗️ Architecture

```
transport-tracker-mvp/
├── backend/                 # Express.js API server
│   ├── routes/             # API route handlers
│   │   ├── busRoutes.js    # Bus route management
│   │   ├── trackingRoutes.js # Real-time tracking
│   │   └── scheduleRoutes.js # Schedule management
│   ├── simulation.js       # GPS simulation system
│   └── server.js          # Main server file
├── frontend/               # Web application
│   ├── index.html         # Main HTML page
│   ├── styles.css         # Optimized CSS styles
│   └── script.js          # JavaScript functionality
├── docs/                  # Documentation
└── README.md             # This file
```

## 🚀 Quick Start

### Prerequisites
- Node.js v16 or higher
- npm package manager

### Installation

1. **Clone and setup the project:**
   ```bash
   git clone <repository-url>
   cd transport-tracker-mvp
   npm install
   cd backend && npm install && cd ..
   ```

2. **Start the application:**
   ```bash
   npm start
   # or for development with auto-reload:
   npm run dev
   ```

3. **Access the application:**
   - Frontend: http://localhost:3000
   - API Health: http://localhost:3000/api/health
   - API Documentation: See API section below

## 🔌 API Documentation

### Base URL
```
http://localhost:3000/api
```

### Endpoints

#### Bus Routes
- **GET** `/buses` - Get all bus routes
- **GET** `/buses/:id` - Get specific bus route
- **POST** `/buses` - Create new bus route (admin)

#### Real-time Tracking
- **GET** `/tracking` - Get all active buses
- **GET** `/tracking/route/:routeId` - Get buses for specific route
- **GET** `/tracking/bus/:busId` - Get specific bus location
- **GET** `/tracking/stop/:stopId/arrivals` - Get arrivals for a stop
- **POST** `/tracking/update/:busId` - Update bus location (GPS device)

#### Schedules
- **GET** `/schedules` - Get all schedules
- **GET** `/schedules/route/:routeId` - Get route schedule
- **GET** `/schedules/departures/:routeId/:stopId` - Get next departures
- **GET** `/schedules/status/:routeId` - Get service status

### Response Format

All API responses follow this format:
```json
{
  "success": true,
  "data": [...],
  "count": 2,
  "message": "Optional message"
}
```

## 📱 Usage Guide

### For Commuters

1. **Select Route**: Choose your bus route from the available options
2. **View Live Tracking**: See real-time bus locations and estimated arrivals
3. **Check Occupancy**: Green/Yellow/Red indicators show how crowded buses are
4. **Auto Updates**: The app refreshes automatically every 30 seconds

### For Transport Authorities

1. **Monitor Fleet**: View all active buses across routes
2. **Track Performance**: Monitor on-time performance and delays
3. **Manage Routes**: Add/modify bus routes and schedules
4. **Update GPS**: Buses can send location updates via API

## 🎮 Demo Data

The MVP includes sample data for testing:

### Routes
- **R1**: City Center → Mall Road → University → Hospital → Railway Station
- **R2**: Main Market → Bus Stand → IT Park Gate → IT Park Center

### Active Buses
- **bus-001**: Route R1, 22/40 passengers
- **bus-002**: Route R1, 35/40 passengers  
- **bus-003**: Route R2, 18/35 passengers

## 🧪 GPS Simulation

The system includes a built-in GPS simulation that:
- Moves buses realistically along routes
- Updates passenger counts at stops
- Generates arrival time estimates
- Simulates GPS coordinate noise
- Handles route reversals at endpoints

### Simulation Controls

Start simulation:
```javascript
const gpsSimulation = require('./backend/simulation');
gpsSimulation.start();
```

Add test bus:
```javascript
gpsSimulation.addBus('1', { 
  speed: 25, 
  currentOccupancy: 20 
});
```

## 🌐 Low-Bandwidth Optimizations

- **Compressed assets** with gzip encoding
- **Minimal payload sizes** (< 10KB per API call)
- **Efficient caching** with 30-second cache headers
- **Optimized images** using SVG icons
- **Request batching** to minimize network calls
- **Offline fallback** with cached data

## 🔧 Configuration

### Environment Variables
Create a `.env` file in the backend directory:

```env
PORT=3000
NODE_ENV=development
API_UPDATE_INTERVAL=30000
SIMULATION_ENABLED=true
```

### Customization

#### Adding New Routes
```javascript
// In backend/routes/busRoutes.js
const newRoute = {
  name: "New Route Name",
  routeNumber: "R3",
  stops: [
    { id: '10', name: 'Stop 1', latitude: 30.7333, longitude: 76.7794 },
    // ... more stops
  ],
  color: '#FF6B6B'
};
```

#### Adjusting Update Frequency
```javascript
// In frontend/script.js
// Change auto-refresh interval (default: 30 seconds)
this.updateInterval = setInterval(() => {
  // ...
}, 15000); // 15 seconds
```

## 🚀 Deployment

### Local Development
```bash
npm run dev
```

### Production Build
```bash
npm start
```

### Docker Deployment
```dockerfile
FROM node:16
WORKDIR /app
COPY package*.json ./
RUN npm install --production
COPY . .
EXPOSE 3000
CMD ["npm", "start"]
```

## 🤝 Contributing

This is an MVP built for the Government of Punjab's transport initiative. To contribute:

1. Fork the repository
2. Create a feature branch
3. Make your changes with tests
4. Submit a pull request

### Development Guidelines
- Keep the low-bandwidth focus
- Test on slow network connections
- Maintain mobile-first design
- Document all API changes

## 📊 Performance Metrics

### Target Performance
- **Initial load**: < 3 seconds on 2G
- **API response time**: < 500ms
- **Update frequency**: 30-second real-time updates
- **Data usage**: < 1MB per hour of usage
- **Battery impact**: Minimal (optimized polling)

### Browser Support
- Chrome 60+
- Firefox 55+
- Safari 12+
- Edge 79+
- Mobile browsers (iOS Safari, Chrome Mobile)

## 🗺️ Roadmap

### Phase 1 (Current MVP)
- ✅ Basic real-time tracking
- ✅ Route management
- ✅ Web interface
- ✅ GPS simulation

### Phase 2 (Future)
- 📱 Progressive Web App (PWA)
- 🗺️ Map integration (OpenStreetMap)
- 🔔 Push notifications for arrivals
- 📈 Analytics dashboard

### Phase 3 (Advanced)
- 🎯 AI-powered delay prediction
- 📍 Crowdsourced bus locations
- 💳 Integration with payment systems
- 🌍 Multi-language support

## 🐛 Troubleshooting

### Common Issues

**Bus locations not updating:**
- Check if GPS simulation is running
- Verify API endpoints are responding
- Check browser network tab for errors

**Slow loading on mobile:**
- Ensure low-bandwidth optimizations are enabled
- Check if service worker is registered
- Verify gzip compression is working

**API errors:**
- Check server logs for detailed error messages
- Verify all npm dependencies are installed
- Ensure correct Node.js version (16+)

## 📞 Support

For technical support or questions:

- **Project Type**: Government Initiative
- **Organization**: Government of Punjab
- **Department**: Department of Higher Education
- **Category**: Software - Transportation & Logistics

## 📄 License

MIT License - see LICENSE file for details.

## 🙏 Acknowledgments

- Government of Punjab for the problem statement
- Urban Mobility India Report 2024 for research data
- Open source community for tools and libraries

---

**Built for small cities, optimized for everyone.** 🚌✨
