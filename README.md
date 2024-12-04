Issues
If we we run above pipeline we will get docker host not found/ is docker deamon running. To fix this we need to update our gitlab-runner config file. It is under /etc/gitlab-runner/config.toml

  [runners.docker]
    tls_verify = false
    image = "ruby:2.7"
    privileged = true – change from false to true
    disable_entrypoint_overwrite = false
    oom_kill_disable = false
    disable_cache = false
    volumes = ["/var/run/docker.sock:/var/run/docker.sock","/cache"] – add docker socket path
    shm_size = 0
    network_mtu = 0

    DOCKER_HOST: "tcp://docker:2375" – “we are using docker service. To connect to it we are                
                                                                                       adding below 3 line”  
    DOCKER_TLS_CERTDIR: "/certs"
    DOCKER_DRIVER: overlay2
--------------------------------------------------
Still we get hostnot found error add below line
        - unset DOCKER_HOST


