# Inside.Io 3D Model Viewer

## Table of Contents

1. [Introduction](#introduction)
2. [System Architecture](#system-architecture)
3. [Frontend Setup](#frontend-setup)
4. [Backend Setup](#backend-setup)
5. [Key Components](#key-components)
6. [Working Principles](#working-principles)
7. [User Guide](#user-guide)
8. [Developer Guide](#developer-guide)
9. [Troubleshooting](#troubleshooting)
10. [Conclusion](#conclusion)

## Introduction

Inside.Io is a comprehensive web-based 3D model viewer application that allows users to upload, view, interact with, and download 3D models in various formats. The application features both a viewer interface for interacting with models and a gallery for browsing available models.

**Key Features:**
- Interactive 3D model viewing with professional-grade controls
- Support for multiple 3D file formats (.obj, .gltf, .glb, .stl)
- Model upload and download capabilities
- Gallery view of available models
- Dark/light theme toggle
- Responsive design

## System Architecture

Inside.Io follows a client-server architecture with:

1. **Frontend**: React application with TypeScript, Three.js, and React Three Fiber
2. **Backend**: Django REST framework serving as an API for model storage and retrieval

### Technology Stack

**Frontend:**
- React + Vite
- TypeScript
- Three.js and React Three Fiber for 3D rendering
- Tailwind CSS for styling

**Backend:**
- Django 5.0.3
- Django REST Framework
- SQLite database (development)

## Frontend Setup

### Prerequisites
- Node.js (v16+)
- npm or yarn

### Installation Steps

1. **Clone the repository:**
   ```bash
   git clone https://github.com/JithinPonduru/Inside.Io-FrontEnd.git
   cd Inside.Io-FrontEnd
   ```

2. **Install dependencies:**
   ```bash
   npm install
   ```

3. **Start development server:**
   ```bash
   npm run dev
   ```

4. **Access the application:**
   Open your browser and navigate to `http://localhost:5173`

### Frontend Structure

```
FrontEnd/
├── src/
│   ├── components/          # React components
│   │   ├── Cube.tsx         # Default model (cube)
│   │   ├── FileUploadButton.tsx
│   │   ├── Footer.tsx
│   │   ├── Gallery.tsx      # Gallery view
│   │   ├── Header.tsx
│   │   └── ModelViewer.tsx  # Main 3D viewer component
│   ├── App.tsx              # Main application component
│   ├── main.tsx             # Entry point
│   └── index.css            # Global styles
├── index.html               # HTML template
├── package.json             # Dependencies and scripts
└── vite.config.ts           # Vite configuration
```

## Backend Setup

### Prerequisites
- Python 3.9+
- pip
- Virtual environment (recommended)

### Installation Steps

1. **Clone the repository or navigate to the Backend folder:**
   ```bash
   cd Inside.Io/BackEnd
   ```

2. **Create and activate a virtual environment:**
   ```bash
   python -m venv venv
   
   # On Windows
   venv\Scripts\activate
   
   # On macOS/Linux
   source venv/bin/activate
   ```

3. **Install dependencies:**
   ```bash
   pip install -r requirements.txt
   ```

4. **Run migrations:**
   ```bash
   python manage.py migrate
   ```

5. **Start the development server:**
   ```bash
   python manage.py runserver
   ```

6. **Access the API:**
   The API will be available at `http://127.0.0.1:8000/api/`

### Backend Structure

```
BackEnd/
├── backend/                 # Django project settings
│   ├── settings.py          # App configurations
│   ├── urls.py              # URL routing
│   └── wsgi.py              # WSGI interface
├── threeDapp/               # Django application
│   ├── migrations/          # Database migrations
│   ├── models.py            # Data models
│   ├── serializers.py       # REST API serializers
│   ├── views.py             # API views
│   └── urls.py              # API endpoints
├── manage.py                # Django management script
└── requirements.txt         # Python dependencies
```

## Key Components

### Frontend Components

#### ModelViewer.tsx
- **Purpose**: Core component for rendering and interacting with 3D models
- **Features**:
  - Model loading and rendering
  - Camera controls (rotation, pan, zoom)
  - Screenshot capture
  - Model export
  - Fullscreen mode
  - Compass indicator for orientation
  - Drag and drop file upload

#### Gallery.tsx
- **Purpose**: Displays available 3D models
- **Features**:
  - Grid layout of model thumbnails
  - Model information display
  - Download options
  - Upload new models

#### Header.tsx and Footer.tsx
- **Purpose**: Navigation and application information
- **Features**:
  - Page navigation
  - Theme toggle
  - Project information

### Backend Components

#### Model3D (models.py)
- **Purpose**: Database model for 3D files
- **Fields**:
  - `file`: FileField for storing the actual 3D model
  - `name`: Model name (extracted from filename)
  - `format`: File format (extracted from extension)

#### Model3DViewSet (views.py)
- **Purpose**: API endpoints for model operations
- **Endpoints**:
  - `GET /api/models/`: List all models
  - `POST /api/models/`: Upload a new model
  - `GET /api/models/{id}/`: Get details of a specific model
  - `GET /api/models/generate_report/`: Generate a report of all models

## Working Principles

### 3D Rendering Process

1. **Model Loading**:
   - The application uses Three.js and React Three Fiber to load and render 3D models
   - Supported formats include .obj, .gltf, .glb, and .stl
   - When no model is loaded, a default rotating cube is displayed

2. **User Interaction**:
   - OrbitControls provide rotation, panning, and zooming capabilities
   - Left click and drag: Rotate the model
   - Right click and drag: Pan the model
   - Scroll wheel: Zoom in/out

3. **Model Upload Process**:
   - User uploads a model via drag-and-drop or file selector
   - Frontend sends file to backend API using FormData
   - Backend validates file format
   - Model is saved to the server's filesystem
   - File metadata is stored in the database

4. **Model Display Process**:
   - Frontend retrieves models from the backend API
   - Models are displayed in the gallery view
   - When selecting a model, it's loaded into the viewer component

## User Guide

### Viewer Mode

1. **Loading a 3D Model**:
   - Drag and drop a 3D model file onto the viewer area
   - Alternatively, click "Upload" in the gallery view

2. **Interacting with the Model**:
   - **Rotate**: Click and drag with left mouse button
   - **Pan**: Click and drag with right mouse button
   - **Zoom**: Use the scroll wheel
   - **Reset**: Click the "Reset" button to return to the default cube

3. **Using Viewer Tools**:
   - **Export**: Download the current model as a GLB file
   - **Screenshot**: Capture the current view as a PNG image
   - **Fullscreen**: Toggle fullscreen mode
   - **Compass**: Use the compass indicator to track model orientation

### Gallery Mode

1. **Browsing Models**:
   - Navigate to the Gallery tab from the header
   - Browse available models with thumbnail previews

2. **Uploading Models**:
   - Click "Upload File" in the gallery view
   - Select a supported 3D model file

3. **Downloading Models**:
   - Click "Download" on any model card to download the file

## Developer Guide

### Adding New Features

#### Adding a New Component

1. Create a new component file in `src/components/`
2. Import and use necessary Three.js or React Three Fiber elements
3. Add the component to the appropriate parent component

#### Modifying the Backend API

1. Update models in `threeDapp/models.py` as needed
2. Create/update serializers in `threeDapp/serializers.py`
3. Add new endpoints in `threeDapp/views.py`
4. Run migrations: `python manage.py makemigrations` followed by `python manage.py migrate`

### Important Integration Points

1. **Frontend-Backend Communication**:
   - API calls are made directly using fetch() in components like Gallery.tsx
   - The backend URL is defined at the top of the Gallery component:
     ```typescript
     const backendUrl = "https://b0ed76d0-7489-42b9-b9b5-02971486301e-00-1qecrwu2j9xei.sisko.replit.dev:8000/api/models/";
     ```
   - Update this URL to match your deployment environment

2. **Three.js Integration**:
   - Three.js is integrated via React Three Fiber
   - Scene setup happens in the ModelViewer component
   - Custom models and controls are defined as React components

## Troubleshooting

### Common Issues and Solutions

1. **CORS Errors**:
   - **Issue**: Browser blocks API requests due to CORS restrictions
   - **Solution**: Ensure Django CORS settings are properly configured in `settings.py`
   ```python
   CORS_ALLOWED_ORIGINS = [
       "http://localhost:5173",  # Development frontend URL
       # Add production URLs as needed
   ]
   ```

2. **Model Loading Failures**:
   - **Issue**: Models fail to load in the viewer
   - **Solution**: 
     - Check the model format is supported (.obj, .gltf, .glb, .stl)
     - Verify file permissions on the server
     - Check browser console for specific errors

3. **Backend Connection Issues**:
   - **Issue**: Frontend cannot connect to the backend API
   - **Solution**:
     - Verify the backend server is running
     - Check the API URL in Gallery.tsx
     - Test API endpoints using tools like Postman

4. **Performance Issues**:
   - **Issue**: Large models render slowly
   - **Solution**:
     - Consider implementing model optimization
     - Add loading indicators for large files
     - Use compressed formats like GLB over OBJ for complex models

## Requirements
- Node.js 16.0 or higher
- Python 3.9 or higher
- Modern web browser with WebGL support

## Contributing
Contributions are welcome! Please feel free to submit a Pull Request.

## License
This project is licensed under the MIT License - see the LICENSE file for details.

## Support
For support, please open an issue on GitHub or contact support@inside.io.

## Conclusion

Inside.Io demonstrates a modern approach to 3D content visualization on the web, combining powerful frontend technologies like Three.js and React with a robust Django backend. This architecture provides a scalable solution for viewing, sharing, and managing 3D models through a web browser.

The system can be extended in various ways:

1. Adding authentication for user-specific galleries
2. Implementing model annotation and collaboration features
3. Adding more advanced 3D tools like measurements and cross-sections
4. Optimizing for mobile devices with touch-friendly controls
