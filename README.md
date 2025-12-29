version: '3'
services:
  # Your existing Speed Test
  speedtest:
    image: linuxserver/librespeed
    container_name: local_speedtest
    ports:
      - 8080:80
    restart: unless-stopped

  # Your new Dashboard
  dashboard:
    image: linuxserver/heimdall
    container_name: heimdall_hub
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Etc/UTC
    ports:
      - 80:80
      - 443:443
    volumes:
      - ./heimdall_config:/config
    restart: unless-stopped
