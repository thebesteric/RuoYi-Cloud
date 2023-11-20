pipeline {
  agent {
    node {
      label 'maven'
    }

  }
  stages {
    stage('拉取代码') {
      agent none
      steps {
        container('maven') {
          sh 'echo 开始拉取代码...'
          git(url: 'https://github.com/thebesteric/RuoYi-Cloud.git', credentialsId: '', branch: 'master', changelog: true, poll: false)
          sh 'echo 代码拉取完成'
          sh 'ls -al'
        }

      }
    }

    stage('项目编译') {
      agent none
      steps {
        container('maven') {
          sh 'echo 开始编译项目...'
          sh 'mvn clean package -Dmaven.test.skip=true'
          sh 'echo 项目编译完成'
        }

      }
    }

    stage('phw6cv') {
      parallel {
        stage('打包ruoyi-gateway镜像') {
          agent none
          steps {
            container('maven') {
              sh 'ls ruoyi-gateway'
              sh 'ls ruoyi-gateway/target'
              sh 'docker build -t ruoyi-gateway:v1 -f ruoyi-gateway/Dockerfile ./ruoyi-gateway'
            }

          }
        }

        stage('打包ruoyi-auth镜像') {
          agent none
          steps {
            container('maven') {
              sh 'ls ruoyi-auth'
              sh 'ls ruoyi-auth/target'
              sh 'docker build -t ruoyi-auth:v1 -f ruoyi-auth/Dockerfile ./ruoyi-auth'
            }

          }
        }

        stage('打包ruoyi-monitor镜像') {
          agent none
          steps {
            container('maven') {
              sh 'ls ruoyi-visual'
              sh 'ls ruoyi-visual/ruoyi-monitor'
              sh 'ls ruoyi-visual/ruoyi-monitor/target'
              sh 'docker build -t ruoyi-monitor:v1 -f ruoyi-visual/ruoyi-monitor/Dockerfile ./ruoyi-visual/ruoyi-monitor'
            }

          }
        }

        stage('打包ruoyi-file镜像') {
          agent none
          steps {
            container('maven') {
              sh 'ls ruoyi-modules/ruoyi-file'
              sh 'ls ruoyi-modules/ruoyi-file/target'
              sh 'docker build -t ruoyi-file:v1 -f ruoyi-modules/ruoyi-file/Dockerfile ./ruoyi-modules/ruoyi-file'
            }

          }
        }

        stage('打包ruoyi-job镜像') {
          agent none
          steps {
            container('maven') {
              sh 'ls ruoyi-modules/ruoyi-job'
              sh 'ls ruoyi-modules/ruoyi-job/target'
              sh 'docker build -t ruoyi-job:v1 -f ruoyi-modules/ruoyi-job/Dockerfile ./ruoyi-modules/ruoyi-job'
            }

          }
        }

        stage('打包ruoyi-system镜像') {
          agent none
          steps {
            container('maven') {
              sh 'ls ruoyi-modules/ruoyi-system'
              sh 'ls ruoyi-modules/ruoyi-system/target'
              sh 'docker build -t ruoyi-system:v1 -f ruoyi-modules/ruoyi-system/Dockerfile ./ruoyi-modules/ruoyi-system'
            }

          }
        }

      }
    }

    stage('ddg7hi') {
      parallel {
        stage('推送ruoyi-gateway镜像') {
          agent none
          steps {
            container('maven') {
              withCredentials([usernamePassword(credentialsId: 'aliyun-docker-registry', passwordVariable: 'ALI_DOCKER_PASSWD', usernameVariable: 'ALI_DOCKER_USER')]) {
                sh 'echo "$ALI_DOCKER_PASSWD" | docker login $REGISTRY -u "$ALI_DOCKER_USER" --password-stdin'
                sh 'docker tag ruoyi-gateway:v1 $REGISTRY/$DOCKERHUB_NAMESPACE/ruoyi-gateway:SNAPSHOT-$BUILD_NUMBER'
                sh 'docker push $REGISTRY/$DOCKERHUB_NAMESPACE/ruoyi-gateway:SNAPSHOT-$BUILD_NUMBER'
              }

            }

          }
        }

        stage('推送ruoyi-auth镜像') {
          agent none
          steps {
            container('maven') {
              withCredentials([usernamePassword(credentialsId: 'aliyun-docker-registry', passwordVariable: 'ALI_DOCKER_PASSWD', usernameVariable: 'ALI_DOCKER_USER')]) {
                sh 'echo "$ALI_DOCKER_PASSWD" | docker login $REGISTRY -u "$ALI_DOCKER_USER" --password-stdin'
                sh 'docker tag ruoyi-auth:v1 $REGISTRY/$DOCKERHUB_NAMESPACE/ruoyi-auth:SNAPSHOT-$BUILD_NUMBER'
                sh 'docker push $REGISTRY/$DOCKERHUB_NAMESPACE/ruoyi-auth:SNAPSHOT-$BUILD_NUMBER'
              }

            }

          }
        }

        stage('推送ruoyi-monitor镜像') {
          agent none
          steps {
            container('maven') {
              withCredentials([usernamePassword(credentialsId: 'aliyun-docker-registry', passwordVariable: 'ALI_DOCKER_PASSWD', usernameVariable: 'ALI_DOCKER_USER')]) {
                sh 'echo "$ALI_DOCKER_PASSWD" | docker login $REGISTRY -u "$ALI_DOCKER_USER" --password-stdin'
                sh 'docker tag ruoyi-monitor:v1 $REGISTRY/$DOCKERHUB_NAMESPACE/ruoyi-monitor:SNAPSHOT-$BUILD_NUMBER'
                sh 'docker push $REGISTRY/$DOCKERHUB_NAMESPACE/ruoyi-monitor:SNAPSHOT-$BUILD_NUMBER'
              }

            }

          }
        }

        stage('推送ruoyi-file镜像') {
          agent none
          steps {
            container('maven') {
              withCredentials([usernamePassword(credentialsId: 'aliyun-docker-registry', passwordVariable: 'ALI_DOCKER_PASSWD', usernameVariable: 'ALI_DOCKER_USER')]) {
                sh 'echo "$ALI_DOCKER_PASSWD" | docker login $REGISTRY -u "$ALI_DOCKER_USER" --password-stdin'
                sh 'docker tag ruoyi-file:v1 $REGISTRY/$DOCKERHUB_NAMESPACE/ruoyi-file:SNAPSHOT-$BUILD_NUMBER'
                sh 'docker push $REGISTRY/$DOCKERHUB_NAMESPACE/ruoyi-file:SNAPSHOT-$BUILD_NUMBER'
              }

            }

          }
        }

        stage('推送ruoyi-job镜像') {
          agent none
          steps {
            container('maven') {
              withCredentials([usernamePassword(credentialsId: 'aliyun-docker-registry', passwordVariable: 'ALI_DOCKER_PASSWD', usernameVariable: 'ALI_DOCKER_USER')]) {
                sh 'echo "$ALI_DOCKER_PASSWD" | docker login $REGISTRY -u "$ALI_DOCKER_USER" --password-stdin'
                sh 'docker tag ruoyi-job:v1 $REGISTRY/$DOCKERHUB_NAMESPACE/ruoyi-job:SNAPSHOT-$BUILD_NUMBER'
                sh 'docker push $REGISTRY/$DOCKERHUB_NAMESPACE/ruoyi-job:SNAPSHOT-$BUILD_NUMBER'
              }

            }

          }
        }

        stage('推送ruoyi-system镜像') {
          agent none
          steps {
            container('maven') {
              withCredentials([usernamePassword(credentialsId: 'aliyun-docker-registry', passwordVariable: 'ALI_DOCKER_PASSWD', usernameVariable: 'ALI_DOCKER_USER')]) {
                sh 'echo "$ALI_DOCKER_PASSWD" | docker login $REGISTRY -u "$ALI_DOCKER_USER" --password-stdin'
                sh 'docker tag ruoyi-system:v1 $REGISTRY/$DOCKERHUB_NAMESPACE/ruoyi-system:SNAPSHOT-$BUILD_NUMBER'
                sh 'docker push $REGISTRY/$DOCKERHUB_NAMESPACE/ruoyi-system:SNAPSHOT-$BUILD_NUMBER'
              }

            }

          }
        }

      }
    }

    stage('部署到dev环境') {
      parallel {
        stage('部署ruoyi-gateway到dev环境') {
          agent none
          steps {
            container('maven') {
              withCredentials([kubeconfigContent(credentialsId: 'demo-kubeconfig', variable: 'VARIABLE')]) {
                sh 'ls -al'
                sh 'envsubst < ruoyi-gateway/deploy.yml | kubectl apply -f -'
              }
            }

          }
        }

      }
    }

    stage('Archive artifacts') {
      steps {
        archiveArtifacts(artifacts: 'target/*.jar', followSymlinks: false)
      }
    }

  }
  environment {
    DOCKER_CREDENTIAL_ID = 'dockerhub-id'
    GITHUB_CREDENTIAL_ID = 'github-id'
    KUBECONFIG_CREDENTIAL_ID = 'demo-kubeconfig'
    REGISTRY = 'registry.cn-hangzhou.aliyuncs.com'
    DOCKERHUB_NAMESPACE = 'wesoft'
    GITHUB_ACCOUNT = 'kubesphere'
    APP_NAME = 'devops-java-sample'
  }
}