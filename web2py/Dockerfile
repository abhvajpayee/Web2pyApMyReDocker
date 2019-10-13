FROM fedora:latest

#LABEL your_label

RUN dnf install -y python3 python3-pip python3-setuptools unzip wget python3-gevent --nogpgcheck && \
 pip3 install --upgrade pip && \
 pip3 install virtualenv 

RUN groupadd -r web2py && \
 useradd -m -r -g web2py web2py

USER web2py

RUN virtualenv /home/web2py && \
 rm -rf /home/web2py/web2py && \
 cd /home/web2py/ && \
 rm -f web2py_src.zip && \
 wget -c http://web2py.com/examples/static/web2py_src.zip && \
 unzip -o web2py_src.zip && \
 rm -rf /home/web2py/web2py/applications/examples && \
 chmod 755 -R /home/web2py/web2py

WORKDIR /home/web2py/web2py

EXPOSE 8000

CMD . /home/web2py/bin/activate && /usr/bin/python3 /home/web2py/web2py/anyserver.py -s gevent -i 0.0.0.0 -p 8000


#FROM python:3.7-slim-stretch
#LABEL AUTHOR "Abhishek Bajpai <abhvajpayee@gmail.com>"

#ENV WEB2PY_ROOT=/opt/web2py

## overridable environment variables
#ENV WEB2PY_VERSION=
#ENV WEB2PY_SERVER="uwsgi"
#ENV WEB2PY_PASSWORD=
#ENV WEB2PY_ADMIN_SECURITY_BYPASS=
#ENV UWSGI_OPTIONS=

#WORKDIR $WEB2PY_ROOT

#RUN apt-get update && apt-get -y install \
#    gcc \
#    git \
#    libpcre3-dev \
# && pip install uwsgi \
# && git clone --recursive https://github.com/web2py/web2py.git $WEB2PY_ROOT \
# && mv $WEB2PY_ROOT/handlers/wsgihandler.py $WEB2PY_ROOT \
# && groupadd -g 1000 web2py \
# && useradd -r -u 1000 -g web2py web2py \
# && chown -R web2py:web2py $WEB2PY_ROOT

#RUN pip install uwsgi pymongo==3.0 pillow pandas numpy 
#RUN pip install gevent 

#COPY entrypoint.sh /usr/local/bin/

#ENTRYPOINT [ "entrypoint.sh" ]
##CMD [ "http" ]
#USER web2py

#EXPOSE 8080 9090
