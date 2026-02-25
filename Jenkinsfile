stage('Deploy NGINX Load Balancer') {
    steps {
        sh '''
        docker rm -f nginx-lb || true

        docker run -d \
          --name nginx-lb \
          --network app-network \
          -p 80:80 \
          nginx

        docker cp nginx/default.conf nginx-lb:/etc/nginx/conf.d/default.conf
        
        docker exec nginx-lb nginx -t
        docker exec nginx-lb nginx -s reload || docker restart nginx-lb
        '''
    }
}
