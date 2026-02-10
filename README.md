# Job Monitor

A single-file Flask dashboard for monitoring SLURM jobs across multiple HPC servers.

![Python](https://img.shields.io/badge/python-3.8+-blue)

## Features

- Displays `squeue` output from multiple servers in a clean web UI
- Color-coded job states (Running, Pending, Completing, Failed, Cancelled)
- Click on a running job to view the last 25 lines of its SLURM output
- Auto-refresh with configurable interval (5s, 10s, 30s, 60s, or off)
- Parallel SSH queries for fast refresh

## Prerequisites

- Python 3.8+
- SSH access to your HPC servers with key-based auth configured in `~/.ssh/config`

## Setup

1. Install Flask:

   ```bash
   pip install flask
   ```

2. Edit `job_monitor.py` and update the `SERVERS` list with your SSH host aliases:

   ```python
   SERVERS = ["juwels", "ferranti"]
   ```

   These should match host entries in your `~/.ssh/config`.

3. Run:

   ```bash
   python3 job_monitor.py
   ```

4. Open http://localhost:5050

## Configuration

| Setting | Location | Default |
|---------|----------|---------|
| Servers | `SERVERS` list in `job_monitor.py` | `["juwels", "ferranti"]` |
| Port | `app.run(port=...)` in `job_monitor.py` | `5050` |
| SSH timeout | `timeout` param in `subprocess.run` calls | `15s` |
| squeue columns | `SQUEUE_FORMAT` in `job_monitor.py` | JOBID, Partition, Name, State, Elapsed, Time Limit, GPUs, Submitted, Nodes, Nodelist |
