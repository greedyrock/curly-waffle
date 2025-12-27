# AnonSpeaks 🎭

**Anonymous Campus Confession Platform**

A modern, feature-rich anonymous social media platform designed for college students to share secrets, confessions, and gossip anonymously. Built with React, Node.js, Express, and MongoDB.

## ✨ Features

- 🎭 **Anonymous Profiles** - Auto-generated anonymous identities for each user
- 📝 **Post Confessions** - Share secrets up to 500 characters
- ❤️ **Like System** - Express support for posts
- 💬 **Comments** - Engage in anonymous discussions
- 🎨 **Modern UI** - Dark theme with gradient accents and smooth animations
- 📱 **Responsive Design** - Works seamlessly on mobile and desktop
- 🔒 **Privacy-First** - Server-side database with secure data handling
- ⚡ **Real-time Updates** - Instant feed refresh after interactions
- 🚀 **Rate Limiting** - Protection against spam and abuse

## 🏗️ Architecture

### Frontend
- **React 18** - Component-based UI
- **Modern CSS** - Custom styling with CSS variables
- **Google Fonts** - DM Serif Display & Inter
- **Responsive Design** - Mobile-first approach

### Backend
- **Node.js & Express** - RESTful API server
- **MongoDB** - NoSQL database for flexible data storage
- **Mongoose** - ODM for MongoDB
- **CORS** - Cross-origin resource sharing
- **Rate Limiting** - Request throttling for security

## 📋 Prerequisites

- Node.js (v14 or higher)
- MongoDB (local or MongoDB Atlas)
- npm or yarn package manager

## 🚀 Quick Start

### 1. Clone or Download Files

Ensure you have these files:
- `index.html` - Frontend application
- `server.js` - Backend API server
- `package.json` - Node.js dependencies
- `.env.example` - Environment configuration template

### 2. Install Dependencies

```bash
npm install
```

This will install:
- express
- mongoose
- cors
- express-rate-limit
- dotenv

### 3. Configure Environment

Copy `.env.example` to `.env`:

```bash
cp .env.example .env
```

Edit `.env` with your configuration:

```env
PORT=3000
MONGODB_URI=mongodb://localhost:27017/anonspeaks
NODE_ENV=development
```

**For MongoDB Atlas (Cloud Database):**
```env
MONGODB_URI=mongodb+srv://username:password@cluster.mongodb.net/anonspeaks?retryWrites=true&w=majority
```

### 4. Start MongoDB (if using local)

```bash
# macOS (using Homebrew)
brew services start mongodb-community

# Linux
sudo systemctl start mongod

# Windows
# MongoDB should start automatically as a service
```

### 5. Start the Backend Server

```bash
npm start
```

Or for development with auto-reload:
```bash
npm run dev
```

You should see:
```
🚀 AnonSpeaks server running on port 3000
📡 API endpoint: http://localhost:3000/api
✅ Connected to MongoDB
```

### 6. Open the Frontend

Open `index.html` in a web browser, or serve it using a local server:

```bash
# Using Python 3
python3 -m http.server 8080

# Using Node.js http-server
npx http-server -p 8080
```

Then visit: `http://localhost:8080`

### 7. Update API URL (if needed)

In `index.html`, line 391, update the API URL if your backend is on a different port:

```javascript
const API_URL = 'http://localhost:3000/api';
```

## 📁 Project Structure

```
anonspeaks/
├── index.html          # Frontend React application
├── server.js           # Backend Express server
├── package.json        # Node.js dependencies
├── .env.example        # Environment variables template
└── README.md          # This file
```

## 🔌 API Endpoints

### Users
- `POST /api/users/create` - Create/retrieve anonymous user

### Posts
- `GET /api/posts` - Get all posts (with pagination)
- `POST /api/posts` - Create a new post
- `POST /api/posts/:postId/like` - Like/unlike a post
- `DELETE /api/posts/:postId` - Delete a post

### Comments
- `POST /api/posts/:postId/comments` - Add a comment to a post

### Health
- `GET /api/health` - Server health check

## 🎨 Design Features

### Color Palette
- Primary Background: `#0a0a0a`
- Secondary Background: `#141414`
- Accent Orange: `#ff6b35`
- Accent Green: `#00d4aa`
- Text Primary: `#ffffff`
- Text Secondary: `#a0a0a0`

### Typography
- Display Font: DM Serif Display (italic)
- Body Font: Inter

### Animations
- Smooth fade-in transitions
- Hover state transformations
- Staggered post loading
- Gradient backgrounds

## 🛡️ Security Features

1. **Rate Limiting** - 100 requests per 15 minutes per IP
2. **Input Validation** - Character limits and required fields
3. **Anonymous IDs** - No personal information stored
4. **CORS Protection** - Configurable allowed origins
5. **Content Length Limits** - Posts: 500 chars, Comments: 300 chars

## 📊 Database Schema

### Posts Collection
```javascript
{
  content: String,           // Post content (max 500 chars)
  anonName: String,          // Anonymous username
  anonColor: String,         // User color hex code
  userId: String,            // Anonymous user ID
  likes: Number,             // Like count
  likedBy: [String],        // Array of user IDs who liked
  timestamp: Date,           // Creation timestamp
}
```

### Comments Collection
```javascript
{
  postId: ObjectId,          // Reference to post
  content: String,           // Comment content (max 300 chars)
  anonName: String,          // Anonymous username
  anonColor: String,         // User color hex code
  userId: String,            // Anonymous user ID
  timestamp: Date,           // Creation timestamp
}
```

### Users Collection
```javascript
{
  userId: String,            // Unique anonymous ID
  anonName: String,          // Generated anonymous name
  anonColor: String,         // Assigned color
  createdAt: Date,           // Account creation date
}
```

## 🌐 Deployment

### Frontend Deployment (Static Hosting)

Deploy `index.html` to:
- **Netlify**: Drag and drop the HTML file
- **Vercel**: Connect Git repo or upload file
- **GitHub Pages**: Push to gh-pages branch
- **AWS S3**: Upload as static website

### Backend Deployment (Node.js Hosting)

Deploy `server.js` to:

#### Heroku
```bash
heroku create anonspeaks-api
git push heroku main
heroku config:set MONGODB_URI=your_mongodb_atlas_uri
```

#### Railway
```bash
railway init
railway add
railway up
```

#### DigitalOcean App Platform
- Connect your Git repository
- Set environment variables in dashboard
- Deploy with one click

#### AWS EC2
```bash
# SSH into instance
ssh -i key.pem ubuntu@your-instance-ip

# Install Node.js
curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -
sudo apt-get install -y nodejs

# Clone and setup
git clone your-repo
cd anonspeaks
npm install
npm start
```

### Database Deployment (MongoDB Atlas)

1. Create account at [mongodb.com/cloud/atlas](https://www.mongodb.com/cloud/atlas)
2. Create a free cluster
3. Add database user
4. Whitelist IP addresses (0.0.0.0/0 for development)
5. Get connection string
6. Update `.env` with connection string

### Environment Variables for Production

```env
PORT=3000
MONGODB_URI=mongodb+srv://username:password@cluster.mongodb.net/anonspeaks
NODE_ENV=production
ALLOWED_ORIGINS=https://yourdomain.com,https://www.yourdomain.com
```

## 🔧 Configuration

### Change Server Port
Edit `.env`:
```env
PORT=5000
```

### Enable HTTPS
Use a reverse proxy like Nginx:
```nginx
server {
    listen 443 ssl;
    server_name api.yourdomain.com;
    
    ssl_certificate /path/to/cert.pem;
    ssl_certificate_key /path/to/key.pem;
    
    location / {
        proxy_pass http://localhost:3000;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }
}
```

### Custom Domain Setup
1. Deploy backend to hosting service
2. Point domain A record to server IP
3. Update `index.html` API_URL with your domain
4. Configure SSL certificate (Let's Encrypt recommended)

## 🐛 Troubleshooting

### MongoDB Connection Issues
```
Error: Failed to connect to MongoDB
```
**Solution:** 
- Check MongoDB is running: `sudo systemctl status mongod`
- Verify connection string in `.env`
- Check firewall settings

### CORS Errors
```
Access to fetch blocked by CORS policy
```
**Solution:**
- Add your frontend URL to `ALLOWED_ORIGINS` in `.env`
- Restart backend server

### Posts Not Appearing
**Solution:**
- Check browser console for errors
- Verify API_URL in `index.html` matches backend
- Check network tab for failed requests

### Rate Limit Exceeded
**Solution:**
- Wait 15 minutes
- Adjust rate limit in `server.js`

## 📱 Mobile Optimization

The app is fully responsive and optimized for:
- iOS Safari
- Android Chrome
- Mobile Firefox
- Progressive Web App (PWA) ready

To enable PWA features, add a `manifest.json` and service worker.

## 🎯 Roadmap

- [ ] Image uploads for posts
- [ ] Post categories/tags
- [ ] Search functionality
- [ ] User blocking
- [ ] Report system
- [ ] Email notifications
- [ ] PWA support
- [ ] Dark/light theme toggle
- [ ] Markdown support
- [ ] Trending posts algorithm

## 📄 License

MIT License - Feel free to use this project for your campus!

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch
3. Commit your changes
4. Push to the branch
5. Create a Pull Request

## 💬 Support

For issues or questions:
- Check the troubleshooting section
- Review API documentation
- Check MongoDB connection
- Verify environment variables

## 🎓 Perfect for:

- College campus confessions
- Anonymous feedback platforms
- Secret sharing communities
- Private discussion forums
- Campus gossip boards

## ⚠️ Important Notes

1. **Privacy**: This platform is anonymous but not untraceable. Consider adding additional security measures for sensitive environments.

2. **Moderation**: Implement content moderation to prevent abuse, harassment, or illegal content.

3. **Scalability**: For large user bases (1000+ concurrent users), consider:
   - Adding Redis for caching
   - Implementing load balancing
   - Database indexing optimization
   - CDN for static assets

4. **Legal**: Ensure compliance with local laws regarding anonymous platforms and user-generated content.

## 🎉 Credits

Built with ❤️ for college communities worldwide.

---

**Made with React, Node.js, Express, and MongoDB**

Enjoy your anonymous campus confession platform! 🎭✨
