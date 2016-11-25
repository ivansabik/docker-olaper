FROM debian:jessie
RUN apt-get update && apt-get install -y wget unzip openjdk-7-jre-headless
RUN wget https://github.com/OSBI/foodmart-data/archive/master.zip -P /tmp && \
    unzip -d /tmp /tmp/master.zip && \
    unzip -d /tmp/foodmart-data-master/data/ /tmp/foodmart-data-master/data/DataScript.zip
RUN wget https://raw.githubusercontent.com/vishnubob/wait-for-it/master/wait-for-it.sh -P /tmp && \
    chmod +x /tmp/wait-for-it.sh

RUN sed -i 's/localhost/db/g' /tmp/foodmart-data-master/FoodMartLoader.sh && \
    chmod +x /tmp/foodmart-data-master/FoodMartLoader.sh

CMD /tmp/wait-for-it.sh db:3306 -- /tmp/foodmart-data-master/FoodMartLoader.sh --db mysql
