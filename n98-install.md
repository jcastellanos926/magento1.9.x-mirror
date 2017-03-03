  
  HOW TO INSTALL MAGENTO WITH N98

  git clone https://github.com/jcastellanos926/magento1.9.x-mirror.git ./ ;

  wget https://raw.githubusercontent.com/Vinai/compressed-magento-sample-data/1.9.1.0/compressed-magento-sample-data-1.9.1.0.tgz ;
  
  tar -xf compressed-magento-sample-data-1.9.1.0.tgz ;
  
  cp -r magento-sample-data-1.9.1.0/* ./ ; 
 
  rm -rf magento-sample-data-1.9.1.0/ ;
  
  n98 local-config:generate -q localhost root root magento files admin;
  
  n98 db:create ;
  
  n98 db:import magento_sample_data_for_1.9.1.0.sql ;
  
  n98 config:set "web/secure/base_url" "http://local.magento.in/" ;

  n98 config:set "web/unsecure/base_url" "http://local.magento.in/" ;
  
  n98 admin:user:create admin magento@jesuscastellanos.com admin Jesús Castellanos ;
  
  n98 customer:create magento@jesuscastellanos.com admin Jesús Castellanos -q ;
  
  n98 admin:notifications ;
  
  n98 design:demo-notice --off --global -q ;

  n98 config:set web/seo/use_rewrites 0 ;

  n98 cache:disable ;nr;nc ;

  rm magento_sample_data_for_1.9.1.0.sql ;

  rm compressed-magento-sample-data-1.9.1.0.tgz ;
  
  chmod -R o+w media var ;
  
  chmod o+w app/etc ;
  
  find . -type d -exec chmod 775 '{}' \;
  
  find . -type f -exec chmod 644 '{}' \;
  
  chmod -R 777 app/etc var/ media/ ;

  rm magento_sample_data_for_1.9.1.0.sql ;

  rm compressed-magento-sample-data-1.9.1.0.tgz ;

  git config core.fileMode false ;

  git gc ;
