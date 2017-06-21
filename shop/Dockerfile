FROM python:3.5

RUN curl -sL https://deb.nodesource.com/setup_4.x | bash -
RUN apt-get install -y build-essential nodejs
RUN npm install -g bower

RUN git clone --depth 1 https://github.com/novirael/django-shop app
WORKDIR /app
RUN pip install -e . && pip install -r requirements/py3/common.txt
RUN npm install
RUN bower --allow-root install

RUN wget http://downloads.django-shop.org/django-shop-workdir.tar.gz
RUN tar zxf django-shop-workdir.tar.gz

WORKDIR /app/example
ENV DJANGO_SHOP_TUTORIAL=polymorphic
ENV DJANGO_DEBUG=1
RUN ./manage.py migrate
RUN ./manage.py loaddata fixtures/myshop-polymorphic.json

EXPOSE 8000
CMD ./manage.py runserver 0.0.0.0:8000

