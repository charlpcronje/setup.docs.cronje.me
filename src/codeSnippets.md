# Install Code Snippets

Just to demonstrate, I will install this with Docker but not Via Portainer

Just run the following command via SSH

```bash
docker run -d --name snippetbox -p 4447:5000 -v /var/www/tools/snippetBox:/app/data pawelmalak/snippet-box
```

- Sometimes when it is a simple `Docker` setup then it's easier to just do this via `SSH` than to do all the effort to login to `Portainer`
- It does not matter oif you add the container here or in Portainer, you will still it in Portainer

Done!
