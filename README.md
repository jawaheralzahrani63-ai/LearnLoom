
# LearnLoom

Online Study Companion web app using Vue.js and AWS Serverless architecture.

## Features
- Upload study notes
- AI-generated summaries, quizzes, and flashcards
- Personalized study schedules and goals
- S3 file storage, Lambda processing
- Comprehend & Polly for summarization and text-to-speech
- DynamoDB for quizzes and study history
- CloudFront for global content delivery
- Cognito authentication
- SNS/SES for daily study reminders


## AWS Architecture (Detailed)

### Frontend
- **Amazon S3**: Hosts the Vue.js static site for global access.
- **Amazon CloudFront**: Distributes content worldwide with low latency and high transfer speeds.
- **Amazon Cognito**: Manages user authentication, authorization, and secure sessions.

### Backend (Serverless API)
- **Amazon API Gateway**: Exposes RESTful endpoints for all app features (notes upload, study goals, quizzes, schedules).
- **AWS Lambda**: Stateless compute functions for:
	- File processing (notes, schedules)
	- AI integration (calls to Comprehend for summarization, Polly for text-to-speech)
	- CRUD operations for quizzes, study history, goals
- **Amazon DynamoDB**: NoSQL database for:
	- Quiz questions
	- Study history
	- User goals and schedules

### AI & Processing
- **Amazon Comprehend**: Analyzes and summarizes uploaded notes.
- **Amazon Polly**: Converts summaries and quizzes to speech for audio flashcards.

### Notifications
- **Amazon SNS/SES**: Sends daily study reminders via email or SMS.

### Security & Monitoring
- **AWS IAM**: Manages roles and permissions for Lambda, API Gateway, S3, DynamoDB, and other resources.
- **Amazon CloudWatch**: Monitors API usage, Lambda execution, and logs errors/events.

### Data Flow Example
1. User uploads notes via frontend (S3 upload, authenticated by Cognito).
2. Lambda triggers to process file, calls Comprehend for summary, Polly for audio.
3. Results stored in DynamoDB; quizzes generated and saved.
4. API Gateway exposes endpoints for CRUD operations (quizzes, goals, schedules).
5. CloudFront serves updated content; SNS/SES sends reminders.
6. IAM secures all resources; CloudWatch logs and monitors activity.

## Getting Started
1. Install dependencies: `npm install`
2. Run development server: `npm run dev`
3. See `copilot-instructions.md` for development workflow

## Deployment
- Frontend: Deploy to S3, serve via CloudFront
- Backend: Deploy Lambda/API Gateway stack via AWS SAM/Serverless Framework

## Notes
- Replace AWS resource placeholders with your actual configuration.
- See documentation for integration details.
