##Convert old httpd image with skopeo
1. dnf install skopeo -y
2. skopeo copy --format v2s2 docker://httpd:2.4.16 docker-daemon:httpd:2.4.16
3. docker images