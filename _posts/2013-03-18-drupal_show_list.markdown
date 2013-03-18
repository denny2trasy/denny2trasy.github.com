---
layout: post
title: Drupal实现节点列表菜单
category: Drupal
---


Drupal有搜索功能，只要在搜索表单中输入条件，点击搜索就可以得到结果列表页面。可是在开发网站的过程中，难免会有这样的需求，一个菜单或者连接实现一个查询。最近在建立[Asischina](http://www.asischia.com)这个网站的时候，就需要实现这个菜单。


具体需求，这个网站中，有一个Node Type是News的节点，想通过/asischina/list/news来得到所有的News列表，并希望结果页面有分页功能。

起初我觉得这个功能不复杂，肯定有Module实现了它，于是就去[Drupal](http://www.drupal.org)官方搜索，结果是令人失望的，两天都没有找到合适的Module。

于是决定自己写个Module实现这个菜单。

+ 定义菜单项,实现hook_menu函数

`	
	$items['asischina/list/%'] = array(
    		'title' => 'Content Type list',
    		'page callback' => 'asischina_list_for_content_type_page',
    		'page arguments' => array(2),
    		'access callback' => TRUE, //array('access content'),
    		'type' => MENU_CALLBACK,
  	);
	return $items;
`


+ 实现查询功能，asischina_list_for_content_type_page($content_type)


`
	$query = 'SELECT nid FROM {node} where type = "'. $content_type .'" ORDER BY nid desc ';
	
	$count_query = "SELECT COUNT(*) FROM (" . $query . ") AS count_query";

	$result = pager_query($query, 10, 0, $count_query);
  
	$output = "";
  
	while ($item = db_fetch_object($result)) {
		
	// Build the node body.
        	$node = node_load($item->nid);

		$output .= node_view($node,true);

  	}
	
	$output .= theme('pager', NULL, 10, 0);	

	return $output;
`


最终代码虽然简单，过程可是很曲折的。

首先，定义菜单项，需要注意page argements与通配符的对应关系，本例中，array(2)对应通配符。

asischina  -- array(0)
list -- array(1)
% -- array[2]

再次，pager_query函数实现分页查询

然后， node_view实现node正确显示，按列表结果展示，不是按full page展示节点

最后， theme('pager',Null,10,0)展示页面中的分页器

纪录这些学习过程。

* * *

*问：github如何得到除master以外的分支*

*答：第一次clone下来都是master,用如下语句可以得到其他分支*

`git checkout -b xxx origin/xxx`



