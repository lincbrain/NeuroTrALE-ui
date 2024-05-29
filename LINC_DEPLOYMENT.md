# Deployment Notes

In May 2024, we evaluated the NeuroTRaLe UI and Data Manager as an annotation tool for
the LINC Project

Here are some notes as to how we deployed:

Within a standard AWS EC2 instance, 2 repositories (NeuroTrALE UI & NeuroTrALE Data Manager) were `git clone` into the `home` directory. 

Following cloning,  2 processes were run in tandem:

(for SNAPSHOT 1.4.0 branch)

1. NeuroTrALE UI via:
```shell
export NODE_OPTIONS=--openssl-legacy-provider && npm run dev
```

2. NeuroTrALE Data Manager (found here: https://github.com/mit-ll/NeuroTrALE-data-manager/tree/main) -- assuming that the `data/precomputed` folder exists already
```shell
docker run -d -p 9000:9000 -v /data/precomputed:/data mitll/precomputed:1.0
```

For the mapping of these processes an `nginx` reverse proxy was set up, with the configuration file linked in this PR

Once this was running, the EC2 instance could be visited with a running app

