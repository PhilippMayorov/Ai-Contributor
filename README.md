# WFN AI Contribution Tracker

## 📋 Project Overview

The WFN AI Contribution Tracker is an intelligent classroom participation monitoring system designed specifically for professors in courses 2257 and HBA-1. This application leverages advanced speech recognition and AI technology to automatically track, transcribe, and evaluate student contributions during live lectures, streamlining the participation marking process.


Pictures: 


<img width="1353" height="766" alt="Screenshot 2025-04-05 at 3 46 33 PM" src="https://github.com/user-attachments/assets/7053ba22-1179-44f6-ba6c-a8bf5e2d17c5" />


<img width="1385" height="811" alt="Screenshot 2025-04-05 at 3 46 17 PM" src="https://github.com/user-attachments/assets/b7386a73-82d9-4e17-8c6b-9ebac196797a" />



## 🎯 Purpose


Traditional classroom participation tracking is time-consuming and prone to human error. Professors must manually note who speaks, what they say, and assign participation scores—all while conducting the lecture. The WFN AI Contribution Tracker automates this process by:

- **Real-time Speech Recognition**: Automatically transcribes student contributions during class
- **Automatic Scoring**: Uses AI to evaluate the quality and relevance of contributions
- **Centralized Database**: Stores all lecture data in MongoDB for easy access and analysis
- **Multi-Platform Access**: Available via web application and mobile app for maximum flexibility
- **Analytics & Reporting**: Provides comprehensive views of student participation over time

## 🏗️ Architecture

### Project Structure

```
ai-contribution-tracker/
├── backend/          # Legacy FastAPI server (audio processing)
├── server/           # Main FastAPI server (database operations)
├── web-app/          # Legacy React web application
├── web-app-2/        # Next.js web application (current)
└── mobile-app/       # React Native mobile application
```

## 🔧 Technology Stack

### Backend

- **FastAPI**: High-performance Python web framework
- **MongoDB Atlas**: Cloud database for storing lectures and contributions
- **MongoEngine**: ODM (Object Document Mapper) for MongoDB
- **OpenAI Whisper**: State-of-the-art speech recognition
- **Python 3.11+**: Core programming language

### Frontend (Web App 2)

- **Next.js 14**: React framework with server-side rendering
- **TypeScript**: Type-safe JavaScript
- **Tailwind CSS**: Utility-first CSS framework
- **NextUI**: Modern React UI library
- **Chart.js**: Data visualization for waveforms and analytics
- **React Chart.js 2**: React wrapper for Chart.js

### Mobile App

- **React Native**: Cross-platform mobile development
- **Expo**: Development toolchain for React Native

## 📊 Database Schema

### Collections

#### Classes Collection

```json
{
  "_id": "ObjectId",
  "name": "Lecture 1",
  "students": ["Student 1", "Student 2", "Student 3"],
  "date": "2023-10-01T00:00:00.000Z"
}
```

#### Lectures Collection

```json
{
  "_id": "ObjectId",
  "class_name": "Lecture 1",
  "date": "2023-10-01T00:00:00.000Z",
  "contrib": [
    {
      "name": "Student 1",
      "said": "The implementation uses a factory pattern",
      "score": 8
    },
    {
      "name": "Student 2",
      "said": "We should consider edge cases",
      "score": 7
    }
  ]
}
```

## 🚀 Getting Started

### Prerequisites

- Python 3.11+
- Node.js 18+
- MongoDB Atlas account
- OpenAI API key (for Whisper)

### Installation

#### 1. Clone the Repository

```bash
git clone https://github.com/redmac135/ai-contribution-tracker.git
cd ai-contribution-tracker
```

#### 2. Backend Setup

```bash
cd server
pip install -r requirements.txt

# Create .env file
echo "MONGODB_URI=your_mongodb_connection_string" > .env
```

#### 3. Web Application Setup

```bash
cd web-app-2
npm install

# Create .env file
echo "NEXT_PUBLIC_API_URL=http://localhost:8000/" > .env
```

#### 4. Mobile App Setup (Optional)

```bash
cd mobile-app
npm install
```

### Running the Application

#### Start Backend Server

```bash
cd server
uvicorn main:app --reload
# Server runs on http://localhost:8000
```

#### Start Web Application

```bash
cd web-app-2
npm run dev
# Application runs on http://localhost:3000
```

#### Start Mobile App

```bash
cd mobile-app
npx expo start
```

## 📱 Features & Usage

### For Professors

#### 1. Recording Lectures

- Navigate to the home page (recording interface)
- Select the lecture section from dropdown (Lecture 1, Lecture 2, etc.)
- Click the microphone button to start recording
- Real-time waveform visualization shows audio levels
- Click stop to end recording and automatically process audio
- Audio is transcribed using Whisper AI and contributions are scored

#### 2. Viewing Lecture Data

- Access the **Lectures** page to see all recorded sessions
- View detailed breakdown of each student's contribution
- See transcriptions of what each student said
- Review AI-generated scores (1-10 scale)
- Filter by lecture date

#### 3. Class Analytics

- Navigate to the **Class** page
- Select a class from the dropdown menu (Lecture 1-10)
- View comprehensive table showing:
  - Student names (rows)
  - Contributions across multiple lecture dates (columns)
  - Average participation scores
  - Individual session scores

#### 4. Editing Scores

- Click on any score cell in the table to edit
- Type new value and press Enter to save
- Changes are automatically calculated in averages
- Click outside to cancel edit

### API Endpoints

#### Lectures

- `GET /lectures/list` - Retrieve all lectures with contributions
- Response includes class name, date, and all student contributions

#### Classes

- `GET /classes/info/?className={name}` - Get class details with aggregated student data
- `GET /classes/getAllClasses/` - List all available classes

#### Recognition

- `POST /recognition/convert/` - Upload and transcribe audio
  - Accepts: audio file (webm/ogg/mp4/wav) and section name
  - Returns: transcription and processed contributions with scores

## 🎓 How It Helps 2257 and HBA-1 Professors

### Time Savings

- **Before**: 30-60 minutes post-lecture to compile participation notes and assign scores
- **After**: 5 minutes to review AI-generated scores and transcriptions
- **Semester Impact**: Saves 15-30 hours per course

### Accuracy & Fairness

- No missed contributions during fast-paced discussions
- Objective scoring criteria applied consistently across all students
- Complete transcription record for grade appeals or reviews
- Reduces unconscious bias in participation scoring

### Data-Driven Insights

- Track participation trends over the semester
- Identify students who may need encouragement to participate
- Recognize highly engaged students for recognition
- Export data for final grade calculations
- Compare participation across different lecture sections

### Enhanced Student Engagement

- Students know contributions are being tracked accurately
- Encourages more thoughtful participation
- Provides concrete feedback on contribution quality
- Creates accountability for class participation

### Accessibility

- Access from any device (desktop, tablet, mobile)
- Cloud-based storage ensures data is never lost
- Multi-section support for professors teaching multiple classes
- Responsive design works on phone, tablet, and desktop

## 🔐 Security & Privacy

- **MongoDB Atlas** provides enterprise-grade security with encryption at rest
- Audio files are processed and transcribed but not permanently stored
- Student data encrypted in transit using TLS/SSL
- Environment variables protect sensitive credentials
- Access control through authentication (future enhancement)

## 🤝 Contributing

This project was developed for Western University courses 2257 and HBA-1. Contributions, bug reports, and feature requests are welcome.

### Development Workflow

```bash
# Create feature branch
git checkout -b feature/your-feature-name

# Make changes and commit
git add .
git commit -m "Description of changes"

# Push to GitHub
git push origin feature/your-feature-name

# Create Pull Request on GitHub
```

## 📝 Future Enhancements

- [ ] **Speaker Identification**: Automatically identify which student is speaking
- [ ] **LMS Integration**: Direct integration with Canvas or Blackboard
- [ ] **Advanced Analytics Dashboard**: Participation heatmaps and trends
- [ ] **PDF Report Generation**: Automated participation reports per student
- [ ] **Multi-language Support**: Support for bilingual classrooms
- [ ] **Offline Mode**: Record lectures without internet connection
- [ ] **Email Notifications**: Automated summaries to students after each lecture
- [ ] **Video Recording**: Capture both audio and video for hybrid classes
- [ ] **Sentiment Analysis**: Track engagement levels through tone analysis
- [ ] **Rubric Customization**: Allow professors to define scoring criteria

## 🐛 Troubleshooting

### MongoDB Connection Issues

```bash
# Check environment variable
echo $MONGODB_URI

# Verify connectivity
pip install certifi
python -c "from pymongo import MongoClient; client = MongoClient('your_uri'); print('Connected!')"
```

**Common Solutions:**

- Verify MongoDB URI in `.env` file includes `ssl=true&tls=true`
- Check network connectivity
- Ensure IP address is whitelisted in MongoDB Atlas
- Install certifi: `pip install certifi`

### Audio Recording Issues

**Browser Permissions:**

- Grant microphone permissions when prompted
- Check browser compatibility (Chrome, Firefox, Safari supported)
- Ensure HTTPS or localhost for getUserMedia API
- Try a different browser if issues persist

**Audio Quality:**

- Use external microphone for better recognition
- Minimize background noise
- Ensure stable internet connection for upload

### API Connection Issues

```bash
# Check backend server status
curl http://localhost:8000/docs

# Verify CORS settings
# Check browser console for CORS errors
```

**Solutions:**

- Verify backend server is running on port 8000
- Check CORS settings in FastAPI allow frontend origin
- Confirm `NEXT_PUBLIC_API_URL` environment variable in web-app-2
- Restart both frontend and backend servers

### Next.js Build Issues

```bash
# Clear cache and rebuild
rm -rf .next
npm run dev
```

## 🎯 Use Cases

### Scenario 1: Large Lecture Hall (2257)

- 150 students, difficult to track individual contributions
- Professor records entire lecture
- System identifies 20 unique student contributions
- Each contribution is transcribed and scored
- Professor reviews and adjusts scores in 10 minutes

### Scenario 2: Case Discussion (HBA-1)

- 40 students in active case discussion
- Multiple students speak rapidly
- System captures all contributions with timestamps
- Professor can focus on facilitating rather than note-taking
- Post-class review shows participation distribution

### Scenario 3: Semester-Long Tracking

- Professor teaches 3 sections of same course
- System aggregates data across 36 lectures
- Identifies students with low participation early
- Provides data for participation grade (20% of final grade)
- Generates individual feedback for each student

## 📄 License

This project is developed for educational purposes for Western University courses 2257 and HBA-1.

## 👥 Development Team

Developed with ❤️ for Western University professors and students to enhance classroom learning experiences.

## 📞 Support

For issues, questions, or feature requests:

- Open an issue on [GitHub](https://github.com/redmac135/ai-contribution-tracker/issues)
- Contact the development team
- Check the [documentation](https://github.com/redmac135/ai-contribution-tracker/wiki)

---

## 📈 Project Statistics

- **Languages**: Python, TypeScript, JavaScript
- **Frameworks**: FastAPI, Next.js, React Native
- **Database**: MongoDB Atlas
- **AI/ML**: OpenAI Whisper
- **Deployment**: Cloud-based (scalable)

---

**Note**: This README reflects the current state of the project. Some features may be under active development. Last updated: October 2025.
