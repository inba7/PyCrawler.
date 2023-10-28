pyspider 
========

A Powerful Spider(Web Crawler) System in Python.

- Write script in Python
- Powerful WebUI with script editor, task monitor, project manager and result viewer
- [MySQL](https://www.mysql.com/), [MongoDB](https://www.mongodb.org/), [Redis](http://redis.io/), [SQLite](https://www.sqlite.org/), [Elasticsearch](https://www.elastic.co/products/elasticsearch); [PostgreSQL](http://www.postgresql.org/) with [SQLAlchemy](http://www.sqlalchemy.org/) as database backend
- [RabbitMQ](http://www.rabbitmq.com/), [Redis](http://redis.io/) and [Kombu](http://kombu.readthedocs.org/) as message queue
- Task priority, retry, periodical, recrawl by age, etc...
- Distributed architecture, Crawl Javascript pages, Python 2.{6,7}, 3.{3,4,5,6} support, etc...


Sample Code 
-----------

```python
from pyspider.libs.base_handler import *


class Handler(BaseHandler):
    crawl_config = {
    }

    @every(minutes=24 * 60)
    def on_start(self):
        self.crawl('http://scrapy.org/', callback=self.index_page)

    @config(age=10 * 24 * 60 * 60)
    def index_page(self, response):
        for each in response.doc('a[href^="http"]').items():
            self.crawl(each.attr.href, callback=self.detail_page)

    def detail_page(self, response):
        return {
            "url": response.url,
            "title": response.doc('title').text(),
        }
```


Installation
------------

* `pip install pyspider`
* run command `pyspider`, visit [http://localhost:5000/](http://localhost:5000/)

**WARNING:** WebUI is open to the public by default, it can be used to execute any command which may harm your system. Please use it in an internal network or [enable `need-auth` for webui](http://docs.pyspider.org/en/latest/Command-Line/#-config).

Quickstart: [http://docs.pyspider.org/en/latest/Quickstart/](http://docs.pyspider.org/en/latest/Quickstart/)

Contribute
----------

* Use It
* [中文问答](http://segmentfault.com/t/pyspider)

TODO
----

### v0.4.0

- [ ] a visual scraping interface like [portia](https://github.com/scrapinghub/portia)