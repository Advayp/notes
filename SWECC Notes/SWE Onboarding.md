# Initial Environment Setup

## Things to Install
- Docker & Docker Desktop
- VSCode
- Git
- Node/Npm
- Python

### Docker Setup
- `docker network create swecc-default`

# Repos
- Make sure you're in the location where you want all your SWECC stuff to be installed
- Would suggest putting all these repos in `~/repos/swecc` - mono repo approach works great here.

## Interview Platform Setup
- **Clone Repo**
	- `git clone https://github.com/swecc-uw/swecc-interview.git`
- **Install dependencies**
	- `npm install`
- **Start application**
	- `npm run dev`

## Server Setup
- **Clone Repo:**
	- `git clone https://github.com/swecc-uw/swecc-server.git`
- **Create virtual environment**
	- `python3 -m venv dev.venv`
- **Add environment variables to dev.venv/bin/activate**
	- Note: you'll need to run `source dev.venv/bin/activate` before you start each service
- **Docker**
	- `docker compose -f docker-compose.dev.yml up --build`
- **Registering a user locally**
	- Ensure the interview platform is running
	- Register an account 
- **Verifying your account locally**
	- `docker ps`
	- `docker exec -it [server-container-id] bash|sh`
	- `cd server`
	- `python manage.py verify_account --username [USERNAME] --discord_id [DISCORD ID]`
- **Making sure your user is an admin**
	- `docker ps`
	- `docker exec -it [server-container-id] bash|sh`
	- `cd server`
	- `python manage.py create_admin --username [username]`

## Additional Repos You May Need
### Backend
- #### [swecc-sockets](https://github.com/swecc-uw/swecc-sockets)
- #### [swecc-bot](https://github.com/swecc-uw/swecc-bot)
- #### [swecc-ai](https://github.com/swecc-uw/swecc-ai)
- #### [swecc-infra](https://github.com/swecc-uw/swecc-infra)

### Frontend
- #### [swecc-engagement](https://github.com/swecc-uw/swecc-engagement)
- #### [swecc-leaderboard](https://github.com/swecc-uw/swecc-leaderboard)
- #### [swecc-resume-review](https://github.com/swecc-uw/swecc-resume-review)



