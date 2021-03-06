# WPQueryBuilder
A query builder for WordPress WP_Query, inspired by the Doctrine Query Builder

[![Build Status](https://travis-ci.org/Simettric/WPQueryBuilder.svg?branch=master)](https://travis-ci.org/Simettric/WPQueryBuilder)

[![SensioLabsInsight](https://insight.sensiolabs.com/projects/63480142-e1dd-40c8-ac7c-24dd82434297/big.png)](https://insight.sensiolabs.com/projects/63480142-e1dd-40c8-ac7c-24dd82434297)

USAGE
=====

### META QUERIES


Retrieve any post type where post meta color value equals to blue OR size meta value equals to XL

           $builder = new Builder();
           $wp_query = $builder->createMainMetaQuery("OR")
                                ->addMetaQuery(MetaQuery::create('color', 'blue'))
                                ->addMetaQuery(MetaQuery::create('size', 'XL'))
                                ->getWPQuery();
                                
                                
Retrieve any post type where post meta price is equal or greater than 10 OR size meta value equals to XL
               
           $builder = new Builder();
           $wp_query = $builder->createMainMetaQuery("AND")
                                ->addMetaQuery(MetaQuery::create('price', 10, '>=', 'NUMERIC'))
                                ->addMetaQuery(MetaQuery::create('size', 'XL'))
                                ->getWPQuery();  
                                
                                
 Retrieve any post type where post meta price is equal or greater than 10 AND (size meta value equals to XL OR post meta color value equals to blue)                              
                                
           $builder = new Builder();
           $builder->createMainMetaQuery("AND")
                   ->addMetaQuery(MetaQuery::create('price', 10, '>=', 'NUMERIC'));
                        
           $condition = new MetaQueryCollection('OR');
           $condition->add(MetaQuery::create('color', 'blue'))
                     ->add(MetaQuery::create('size', 'XL'));
                     
                     
           $wp_query = $builder->addMetaQueryCollection($condition)
                               ->getWPQuery();  

### POST TYPES

Retrieve all PAGES

           $builder = new Builder();
           $wp_query = $builder->addPostType(Builder::POST_TYPE_PAGE)->getWPQuery();
           
Retrieve all CUSTOM POST TYPE

           $builder = new Builder();
           $wp_query = $builder->addPostType('your_custom')->getWPQuery();
           
Retrieve all CUSTOM POST TYPE and PAGES

           $builder = new Builder();
           $wp_query = $builder->addPostType('your_custom')
                               ->addPostType(Builder::POST_TYPE_PAGE)
                               ->getWPQuery();
                               
      
### ORDERBY

Order contents by title descending

            $builder = new Builder();
    
            $wp_query = $builder->addOrderBy("title")->getWPQuery();
            
           
Order contents by title with date fallback, ascending

            $builder = new Builder();
    
            $wp_query = $builder->addOrderBy("title")
                                ->addOrderBy("date")
                                ->setOrderDirection("ASC")
                                ->getWPQuery();
                                
            
            
### LIMITS AND OFFSETS

Retrieve only 10 contents

            $builder = new Builder();
    
            $wp_query = $builder->setLimit(10)->getWPQuery();
            
           
Retrieve 20 contents starting from the 10th position

            $builder = new Builder();
    
            $wp_query = $builder->setLimit(20)->setOffset(10)->getWPQuery();

### RETRIEVING


Get the WPQuery object

            $builder = new Builder();
    
            $wp_query = $builder->getWPQuery();
            
            
Get the Posts array

            $builder = new Builder();
    
            $posts = $builder->getPosts();
            
            
Get the WPQuery parameters array

            $builder = new Builder();
    
            $params = $builder->getParameters();
            
            $query = new WP_Query($params);
