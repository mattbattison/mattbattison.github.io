pipeline {
	agent none
	stages {
		stage('Prepare') {
			agent {
				docker {
					image 'ruby'
					args '-v bundler:/usr/local/bundle'
				}
			}
			stages {
				stage('Install Dependencies') {
					steps {
						sh 'gem install bundler'
						sh 'bundle install'
					}
				}
				stage('Build') {
					steps {
						sh 'bundle exec jekyll build'
					}
				}
			}
			post {
				success {
					dir('_site') {
						stash 'site'
					}
				}
			}
		}
		stage('Deploy') {
			agent any
			steps {
				sh 'rm -rf /var/www/html/mattbattison.github.io/'
				sh 'mkdir -p /var/www/html/mattbattison.github.io/'
				dir ('/var/www/html/mattbattison.github.io/') {
					unstash 'site'
				}
			}
		}
	}
}
