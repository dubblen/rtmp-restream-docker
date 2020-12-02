# RTMP restream docker

Ready to deploy Nginx with rtmp module and stunnel in docker-compose



### Getting started

Edit **nginx.conf** located in ./containers/rtmp/conf and supply your RTMP keys for your social networks.

```
worker_processes auto;
rtmp_auto_push on;
events {}
rtmp {
    server {
        listen 1935;
        listen [::]:1935 ipv6only=on;

        application live {
            live on;
            push_reconnect 1s;
            record off;
            push 'rtmp://stunnel:4433/rtmp/<FB_RTMP_KEY>';
            push 'rtmp://a.rtmp.youtube.com/live2/<YOUTUBE_RTMP_KEY>';
        }
        application source {
            live on;
            record off;
        }
    }
}
```

Start up your docker-compose

```bash
cd path/to/rtmp-restream-docker
docker-compose up
```

Connect your streaming software to your restream server

![](/home/madeta/projects/docker-rtmp-restream/obs1.png)

And you are ready to stream!