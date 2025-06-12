# Remark42 Comment System

A self-hosted comment system using Remark42 with Docker Compose.

## Prerequisites

- Docker and Docker Compose installed
- Gmail account with App Password (for email notifications)

## Quick Start

### 1. Clone and Setup

```bash
git clone <your-repo-url>
cd <project-directory>
```

### 2. Environment Configuration

Copy the appropriate environment file:

**For Development:**
```bash
cp .env.dev .env
```

**For Production:**
```bash
cp .env.prod .env
```

### 3. Configure Environment Variables

Edit your `.env` file and update the following variables:

```bash
# Required: Update these values
SECRET=your-strong-secret-here
SMTP_USERNAME=your-email@gmail.com
SMTP_PASSWORD=your-gmail-app-password
AUTH_EMAIL_FROM=your-email@gmail.com
NOTIFY_EMAIL_FROM=your-email@gmail.com

# For production, also update:
REMARK_URL=https://yourdomain.com
```

### 4. Generate Strong Secret

Generate a secure secret key:
```bash
openssl rand -base64 32
```

Copy the output and replace the `SECRET` value in your `.env` file.

### 5. Gmail App Password Setup

1. Enable 2-factor authentication on your Gmail account
2. Go to Google Account settings → Security → App passwords
3. Generate an app password for "Mail"
4. Use this password as `SMTP_PASSWORD` in your `.env` file

## Running the Application

### Development Mode

```bash
# Using specific env file
docker-compose --env-file .env.dev up

# Or using default .env
docker-compose up
```

### Production Mode

```bash
# Using specific env file
docker-compose --env-file .env.prod up -d

# Or using default .env
docker-compose up -d
```

```

## Accessing the Application

- **Development**: http://127.0.0.1:8080
- **Production**: https://spmods.org:8080

## File Structure

```
├── docker-compose.yml          # Main Docker Compose configuration
├── .env.dev                   # Development environment variables
├── .env.prod                  # Production environment variables
├── .env.example              # Example environment file
├── nginx.conf                # Nginx reverse proxy configuration
├── remark.css               # Custom CSS styling
├── var/                     # Remark42 data directory
└── README.md               # This file
```

## Configuration Options

### Environment Variables

| Variable | Description | Example |
|----------|-------------|---------|
| `REMARK_URL` | Public URL of your site | `https://yourdomain.com` |
| `SECRET` | Secret key for JWT tokens | `generated-32-char-hex` |
| `SMTP_USERNAME` | Gmail username | `your-email@gmail.com` |
| `SMTP_PASSWORD` | Gmail app password | `16-char-app-password` |
| `AUTH_EMAIL_FROM` | Email address for auth emails | `your-email@gmail.com` |
| `NOTIFY_EMAIL_FROM` | Email address for notifications | `your-email@gmail.com` |
| `DEBUG` | Enable debug mode | `true` / `false` |

### Key Features Enabled

- Email authentication
- Email notifications
- SMTP via Gmail
- SSL/TLS encryption
- Reverse proxy with Nginx

## Troubleshooting

### Common Issues

1. **Port 8080 already in use:**
   ```bash
   # Check what's using the port
   lsof -i :8080
   
   # Kill the process or change the port in docker-compose.yml
   ```

2. **Email not working:**
   - Verify Gmail app password is correct
   - Check 2FA is enabled on Gmail account
   - Ensure SMTP settings match Gmail requirements

3. **Permission issues:**
   ```bash
   # Fix permissions for data directory
   sudo chown -R $USER:$USER ./var
   ```

4. **Container won't start:**
   ```bash
   # Check logs
   docker-compose logs remark
   
   # Check container status
   docker-compose ps
   ```

### Useful Commands

```bash
# View logs
docker-compose logs -f remark

# Restart services
docker-compose restart

# Stop services
docker-compose down

# Stop and remove volumes
docker-compose down -v

# Update to latest image
docker-compose pull
docker-compose up -d
```

## Security Notes

- Never commit `.env*` files to version control
- Use strong, unique secrets in production
- Regularly rotate SMTP passwords
- Keep Docker images updated
- Use HTTPS in production

## Support

For Remark42 specific issues, check the [official documentation](https://remark42.com/) or [GitHub repository](https://github.com/umputun/remark42).

## License

[Add your license information here]
