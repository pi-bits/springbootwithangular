    git submodule update --recursive --remote
    git submodule update --init --recursive
    #pull all changes in the repo including changes in the submodules   
    git pull --recurse-submodules
    # pull all changes for the submodules
    git submodule update --remote
    
1. Create angular application in src/main/resources/front-end/angular-app

2. Run "npm install" in the angular-app - this can be git submodule as well.

3. Change the output path in the angular.json to public for the build phase.

		{
		  "$schema": "./node_modules/@angular/cli/lib/config/schema.json",
		  "version": 1,
		  "newProjectRoot": "projects",
		  "projects": {
		    "angular-app": {
		      "root": "",
		      "sourceRoot": "src",
		      "projectType": "application",
		      "prefix": "app",
		      "schematics": {},
		      "architect": {
			"build": {
			  "builder": "@angular-devkit/build-angular:browser",
			  "options": {
			    "outputPath": "../public",
			    "index": "src/index.html",
			    "main": "src/main.ts",
			    "polyfills": "src/polyfills.ts",
			    "tsConfig": "src/tsconfig.app.json",
			    "assets": [
			      "src/favicon.ico",
			      "src/assets"
			    ],
			    "styles": [
			      "src/styles.css"
			    ],
			    "scripts": []
			  }

		}

4. Add maven plugin exec-maven-plugin before building the Spring boot application (i.e validate phase) to "run ng build"
5. In the plugin configuration set working directory(workingDirectory) to   src/main/resources/front-end/angular-app

Example:

        <plugin>
				<groupId>org.codehaus.mojo</groupId>
				<artifactId>exec-maven-plugin</artifactId>
				<version>1.6.0</version>
				<executions>
					<execution>
						<phase>validate</phase>
						<goals>
							<goal>exec</goal>
						</goals>
					</execution>
				</executions>
				<configuration>
					<executable>ng</executable>
					<workingDirectory>src/main/resources/front-end/angular-app</workingDirectory>
					<arguments>
						<argument>build</argument>
					</arguments>
				</configuration>
			</plugin>        
       
  6. Run "mvn clean install"
  7. Run java -jar "jarname" 
  8. Angular application should be served on port 8080
           
