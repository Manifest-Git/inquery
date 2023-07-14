<div align="center">
<a href="https://inquery.io"><img src="https://svgshare.com/i/qxX.svg" alt="Inquery"></a>

<em>Superpowers for your SQL database</em>

[![Twitter](https://img.shields.io/twitter/url/https/twitter.com/inqueryio.svg?style=social&label=Follow%20%40inqueryio)](https://twitter.com/inqueryio)
[![GitHub Repo stars](https://img.shields.io/github/stars/inqueryio/inquery?style=social)](https://github.com/inqueryio/inquery)
[![FOSSA Status](https://app.fossa.com/api/projects/git%2Bgithub.com%2FManifest-Git%2Finquery.svg?type=shield)](https://app.fossa.com/projects/git%2Bgithub.com%2FManifest-Git%2Finquery?ref=badge_shield)

<h3>
    <a href="https://docs.inquery.io">Docs</a> |
    <a href="https://join.slack.com/t/inqueryio/shared_invite/zt-1psu47idh-vnItf_BaWcIWih8flGZ0fw">Slack</a> |
    <a href="https://inquery.io">Website</a> 
</h3>

</div>

## Inquery is an open-source toolkit for SQL databases, starting with PostgreSQL

* **[Alerts](#alerts):** Receive notifications when a change occurs
* **[Audit History](#audit-history-beta):** View all historical changes with context
* **[Query Preview](#query-preview-coming-soon):** Preview affected rows and query plan prior to running changes
* **[Approval Flow](#approval-flow-coming-soon):** Require query review before a change can be run
* **[Branching](#):** Git-like version control
* **[Instant Rollback](#):** Instantly rollback to any commit

## Alerts

Alerts can be used to send notifications when a database change is made (INSERT, UPDATE, DELETE).

* Send notifications to Slack, email, or any other webhook
* Filter-out changes made by application users to only see manual updates
* Use template strings (column values, user, etc.) to see what was changed and by who

### How It Works

1. Data is modified in a Postgres table (INSERT, UPDATE, DELETE)
2. A Postgres trigger notifies the Inquery web server via a websocket message
3. Inquery formats, filters, and sends the data to configured webhook(s)

![Inquery Create Slack Notification](https://i.imgur.com/1xoorz9.gif)

## Audit History (beta)

View all manual data updates that occurred in your Postgres database, even those that weren't initiated through the
Inquery UI.

## Query Preview (coming soon)

Before executing a query, check which tables and rows will be affected. View exactly which columns will be updated and
their new value. Explore the visual query plan generated from EXPLAIN.

## Approval Flow (coming soon)

Submit a query for approval by teammates instead of running them directly against the production database. Auto-approval
rules can be configured based on the number of rows changed, the table being updated, or the user's role.

![Inquery Approval Flow Mockup](https://i.imgur.com/5I3Nl6p.png)

## Get Started

### Run Inquery locally

You can run Inquery locally with Docker.

```bash
git clone --depth 1 https://github.com/inqueryio/inquery.git
cd inquery
docker-compose up -d
```

Then open [http://localhost:3000](http://localhost:3000) to access Inquery.
<br>
<br>
**Note**: When connecting your database, if your Postgres host is `localhost`, you must use `host.docker.internal`
instead to access it when running with Docker.

### Run Inquery on AWS (EC2)

**Note**: Make sure this instance is only accessible within your VPC.\
**Note**: Make sure your local machine is able to connect to the server on port 3000 (the web server) and 3003 (the API server) over HTTP.\
**Note**: These instructions are for Amazon Linux 2 AMI (HVM).

1. To install Docker, run the following command in your SSH session on the instance terminal:

```bash
sudo yum update -y
sudo yum install -y docker
sudo service docker start
sudo usermod -a -G docker $USER
logout # Needed to close the SSH session so Docker does not have to be run as root
```

2. To install `docker-compose`, run the following command in your ssh session on the instance terminal:

```bash
sudo curl -L "https://github.com/docker/compose/releases/download/v2.16.0/docker-compose-$(uname -s)-$(uname -m)"  -o /usr/local/bin/docker-compose
sudo mv /usr/local/bin/docker-compose /usr/bin/docker-compose
sudo chmod +x /usr/bin/docker-compose
docker-compose version
```

3. Install and run Inquery

```bash
mkdir inquery && cd inquery
wget https://raw.githubusercontent.com/inqueryio/inquery/main/{.env,docker-compose.yml,.dockerignore,frontend.env}
docker-compose up -d
```

### Run Inquery Cloud (Beta)

Sign up for [Inquery Cloud](https://www.inquery.io/sign-up) early access and get a managed, cloud-hosted instance.


## Get In Touch
Let us know your feedback or feature requests! You can submit a GitHub issue or contact us
at [hey@inquery.io](mailto:hey@inquery.io).


## License
[![FOSSA Status](https://app.fossa.com/api/projects/git%2Bgithub.com%2FManifest-Git%2Finquery.svg?type=large)](https://app.fossa.com/projects/git%2Bgithub.com%2FManifest-Git%2Finquery?ref=badge_large)