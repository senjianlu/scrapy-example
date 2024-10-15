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
下载后解压，得到这样的目录结构：  
![目录结构](https://image.senjianlu.com/blog/2024-10-15/simple_project.png)  

```text
scrapy-example
├── .gitignore
├── README.md
├── requirements.txt
└── my_example_spiders
    ├── scrapy.cfg
    └── my_example_spiders
        ├── __init__.py
        ├── items.py
        ├── middlewares.py
        ├── pipelines.py
        ├── settings.py
        └── spiders
            ├── __init__.py
            └── quotes.py
```

**需要上传的是 `scrapy-example-master` 下面的 `my_example_spiders` 目录**（更上层一点的 `my_example_spiders` 目录）。

在页面上新建爬虫：  
- 名称：`my_example_spiders`
- 执行命令：`scrapy crawl quotes`

![新建爬虫](https://image.senjianlu.com/blog/2024-10-15/new_spider2.png)  

之后进入爬虫，点击上传：  
![点击上传按钮](https://image.senjianlu.com/blog/2024-10-15/upload_spider2.png)  
![选择 my_example_spiders 目录](https://image.senjianlu.com/blog/2024-10-15/upload_spider_files2.png)  

上传成功后，在左侧文件列表中可以双击打开文件：  
![上传成功](https://image.senjianlu.com/blog/2024-10-15/upload_success2.png)  

#### 2、运行爬虫
点击爬虫的运行按钮：  
![运行](https://image.senjianlu.com/blog/2024-10-15/click_run_button2.png)  
![开始](https://image.senjianlu.com/blog/2024-10-15/spider_start.png)  

稍等片刻不出以外会成功：  
![运行成功](https://image.senjianlu.com/blog/2024-10-15/spider_success.png)  
> 如果出现 `File not found` 或是 `undefined` 之类的错误，大概率是你的爬虫目录上传错了。  

前往任务菜单，可以找到对应执行的日志：  
![点击查看日志](https://image.senjianlu.com/blog/2024-10-15/log.png)  
![详细日志](https://image.senjianlu.com/blog/2024-10-15/more_log.png)

点击数据可以看到相关的爬取结果：  
![数据](https://image.senjianlu.com/blog/2024-10-15/data.png)  
视情况导出：  
![导出数据](https://image.senjianlu.com/blog/2024-10-15/output.png)