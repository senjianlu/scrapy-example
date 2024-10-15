# scrapy-example
Scrapy 爬虫样例。

## 项目构成流程
创建名为 `my_example_spiders` 的爬虫项目：
```bash
scrapy startproject my_example_spiders
```
进入项目并创建针对 `quotes.toscrape.com` 网站的爬虫 `quotes`：
```bash
cd my_example_spiders
scrapy genspider quotes quotes.toscrape.com
```
之后修改 `quotes.py` 文件，添加爬虫逻辑。

## 项目运行
### 一、本地运行
在 `my_example_spiders`目录下运行爬虫：
```bash
scrapy crawl quotes
```
> 出现以下错误是正常情况：
> ```bash
> 2024-10-15 05:15:48 [twisted] CRITICAL: Unhandled error in Deferred:
> 2024-10-15 05:15:48 [twisted] CRITICAL: 
> Traceback (most recent call last):
>   File "/usr/local/python/3.12.1/lib/python3.12/site-packages/scrapy/utils/misc.py", line 82, in load_object
>     obj = getattr(mod, name)
>           ^^^^^^^^^^^^^^^^^^
> AttributeError: module 'crawlab' has no attribute 'CrawlabPipeline'
> 
> During handling of the above exception, another exception occurred:
> 
> Traceback (most recent call last):
>   File "/usr/local/python/3.12.1/lib/python3.12/site-packages/twisted/internet/defer.py", line 2014, in _inlineCallbacks
>     result = context.run(gen.send, result)
>   File "/usr/local/python/3.12.1/lib/python3.12/site-packages/scrapy/crawler.py", line 158, in crawl
>     self.engine = self._create_engine()
>   File "/usr/local/python/3.12.1/lib/python3.12/site-packages/scrapy/crawler.py", line 172, in _create_engine
>     return ExecutionEngine(self, lambda _: self.stop())
>   File "/usr/local/python/3.12.1/lib/python3.12/site-packages/scrapy/core/engine.py", line 101, in __init__
>     self.scraper = Scraper(crawler)
>   File "/usr/local/python/3.12.1/lib/python3.12/site-packages/scrapy/core/scraper.py", line 109, in __init__
>     self.itemproc: ItemPipelineManager = itemproc_cls.from_crawler(crawler)
>   File "/usr/local/python/3.12.1/lib/python3.12/site-packages/scrapy/middleware.py", line 90, in from_crawler
>     return cls.from_settings(crawler.settings, crawler)
>   File "/usr/local/python/3.12.1/lib/python3.12/site-packages/scrapy/middleware.py", line 66, in from_settings
>     mwcls = load_object(clspath)
>   File "/usr/local/python/3.12.1/lib/python3.12/site-packages/scrapy/utils/misc.py", line 84, in load_object
>     raise NameError(f"Module '{module}' doesn't define any object named '{name}'")
> NameError: Module 'crawlab' doesn't define any object named 'CrawlabPipeline'
> ```
> 该错误是由于 `settings.py` 文件中的 `ITEM_PIPELINES` 配置项中的 `crawlab.CrawlabPipeline` 未定义，可以忽略。

### 二、通过 Crawlab 运行
#### 1、创建爬虫
