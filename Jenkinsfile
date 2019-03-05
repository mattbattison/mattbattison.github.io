pipeline {
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
			sh 'tar -cvzf site.tar.gz _site'
			archiveArtifacts artifacts: 'site.tar.gz'
		}
	}
}
