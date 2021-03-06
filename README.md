To get started with using Globalization service you need to fork this project
and change the credentials to your own credentials.

Once you have this project up and running with the Liberty for Java runtime and the Globalization,
Watson Machine, AlchemyAPI, and IBM Insights for Twitter services bound to the application you can go
ahead and select a best sellers list. The application will then display the best sellers information
translated into the language you selected.

The Book Club application contains the following contents:


*   src/main/webapp

    This directory contains the client side code (HTML/CSS/JavaScript/Java Server Pages) of the Book Club application.

*   src/main/java

    This directory contains the server side code (JAVA) of the Book Club application.

*   pom.xml

    This file builds the Book Club application using Maven.


This sample application demonstrates how to use the Globalization service in a
Java Web application (powered by WebSphere Liberty) and deploy it on Bluemix.

1. [Install the cf command-line tool](${doc-url}/#starters/BuildingWeb.html#install_cf).

2. Create a new WebSphere Liberty based application in the Bluemix dashboard and select
a name and route for the application. The name and route that you select
will be used to access the application.

3. If you wish to build and deploy this application from your own system, then fork and pull this
repository to your local system.

4. If you are going to build and deploy directly from your system, then connect to Bluemix:

		cf api ${api-url}

5. If you are going to build and deploy directly from your system, then log into Bluemix:

		cf login -u ${username}
		cf target -o ${org} -s ${space}

6. Create and bind the Globalization, Watson Machine Translation, and IBM Insights for Twitter services
to the application that you just created. The names you select for the services will be used in the
deploy script.

7. Obtain api keys for the New York Times Best Sellers, iDreamBooks, and AlchemyAPI services:

		http://developer.nytimes.com
		http://idreambooks.com/api
		http://www.alchemyapi.com

8. If you want to build the application in IBM DevOps Services, then add a Stage from the "Build & Deploy" tab with a Build job type using the maven builder. Use the default archive directory of target.
Otherwise build the application from your command line:

		mvn package

9. If you want to deploy the application from IBM DevOps services, then add a Stage from the "Build & Deploy" tab wih a Deploy job type. Fill in the fields for your Bluemix organization, space, and application name.

10. If you are deploying the application from IBM DevOps services, then Edit the deploy script
and fill in your credentials for the New York Times, iDreamBooks, and IBM AlchemyAPI services
and names that you have used for the Watson MT, Globalization, and Insights for Twitter services.
If you are deploying directly from your command line then you will need to substitute the name of the application
in place of the ${CF_APP} environment variable.

		cf push "${CF_APP}" -p BookClub-1.0-SNAPSHOT.war -m 768M --no-start
		cf bind-service "${CF_APP}" "Watson Language Translator service name"
		cf bind-service "${CF_APP}" "Globalization service name"
		cf bind-service "${CF_APP}" "Insights for Twitter service name"
		cf set-env "${CF_APP}" NY_TIMES_URL api.nytimes.com
		cf set-env "${CF_APP}" NY_TIMES_API_KEY "api key"
		cf set-env "${CF_APP}" DREAM_BOOKS_URL idreambooks.com
		cf set-env "${CF_APP}" DREAM_BOOKS_API_KEY "api key"
		cf set-env "${CF_APP}" ALCHEMY_API_KEY "api key"
		cf start "${CF_APP}"

11. Access your app: [http://${route}](http://${route})
