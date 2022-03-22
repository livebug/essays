# Docker 安装 Mysql

1. 拉取最新镜像
```shell
docker pull mysql:latest
```
2. 运行容器
```shell
docker run -itd --name mysql-test -p 3306:3306 -e MYSQL_ROOT_PASSWORD=111222 mysql
```

    -p 3306:3306 ：映射容器服务的 3306 端口到宿主机的 3306 端口，外部主机可以直接通过 宿主机ip:3306 访问到 MySQL 的服务。
    MYSQL_ROOT_PASSWORD=123456：设置 MySQL 服务 root 用户的密码。 

# 使用DB2数据库

1. 创建 SHADB 数据库 

    db2 create database SHADB using codeset utf-8 territory CN

    + 查看数据库

        db2 list db directory

    + 激活数据库 “XYZ”。
    
        db2 activate db SHADB


2. 创建用户 （管理员）sha/sha （查询权限）shalook/shalook

    useradd -g db2iadm1 -u sha
    db2 grant dbadm on shadb to user sha


    + 现在验证数据库的权限:

        db2 "select substr(authority,1,25) as authority, d_user, d_group, d_public, role_user, role_group, role_public,d_role from table(sysproc.auth_list_authorities_for_authid ('public','g'))as t order by authority"

    + 缓冲池大小

        db2 "select * from syscat.bufferpools"

3. 建库脚本

    ```sql
    /*
    中国城乡代码格式详解
    第1-2位表示省（自治区、直辖市、特别行政区）。
    第3-4位表示市（地级市、自治州、盟及国家直辖市所属市辖区和县的汇总码）。其中，01-20，51-70表示省直辖市；21-50表示地区（自治州、盟）。
    第5-6位表示县（市辖区、县级市、旗）。01-18表示市辖区或地区（自治州、盟）辖县级市；21-80表示县（旗）；81-99表示省直辖县级市。
    第7-9位表示镇（乡镇、街道办事处、乡、特殊区、特殊农场、特殊公司）。
    第9-12位表示村（农村村委会、社区居委会、虚拟社区、特殊团部、特殊连）。
    例如代码：320508019044，32代表江苏省，05代表苏州市，08代表姑苏区，019代表金阊街道，044代表养育巷社区居委会。 
    */

    CREATE TABLE AreaCode (
    TYPE        varchar(1)  NOT NULL,  -- 地区级别 1 省/直辖市 2 地级市 3 区/县/县级市 4/镇/乡/街道 5 村/社区
    code        varchar(12)  NOT NULL, -- 地区代码 
    name        varchar(255)  NOT NULL,-- 名称
    parent_code varchar(12) ,          -- 上级代码
    short_code  varchar(12)  NOT NULL, -- 简码
    catalog     varchar(255)  ,        -- 乡村分类
    sub         INTEGER ,           --下级数量
    Version     varchar(4),            -- 版本号
    DARTETIME   TIMESTAMP,
    PRIMARY KEY (code)
    );
    COMMIT;
    COMMENT ON TABLE "SHA     "."AREACODE" IS '中国地区代码' ;
    COMMENT ON COLUMN "SHA     "."AREACODE"."CATALOG" IS '乡村分类' ;
    COMMENT ON COLUMN "SHA     "."AREACODE"."CODE" IS '地区代码' ;
    COMMENT ON COLUMN "SHA     "."AREACODE"."NAME" IS '地区名称' ;
    COMMENT ON COLUMN "SHA     "."AREACODE"."PARENT_CODE" IS '上级代码' ;
    COMMENT ON COLUMN "SHA     "."AREACODE"."SHORT_CODE" IS '简码' ;
    COMMENT ON COLUMN "SHA     "."AREACODE"."SUB" IS '下级数量' ;
    COMMENT ON COLUMN "SHA     "."AREACODE"."TYPE" IS '地区级别 1 省/直辖市 2 地级市 3 区/县/县级市 4/镇/乡/街道 5 村/社区' ;
    COMMENT ON COLUMN "SHA     "."AREACODE"."VERSION" IS '版本号' ;
    GRANT CONTROL ON TABLE "SHA     "."AREACODE" TO USER "SHA     "  ;
    COMMIT;


    -- 测试查询
    SELECT SUBSTR(CODE,1,1),count(1) FROM AREACODE a GROUP BY SUBSTR(CODE,1,1) ;

    -- 测试插入
    INSERT INTO SHA.AREACODE ("TYPE", CODE, NAME, PARENT_CODE, SHORT_CODE, "CATALOG", SUB) VALUES ('1', '110000000000', '北京市', NULL, '11', NULL, 1);

    --db2 "import from ./area2019.txt of del commitcount 100000 insert_update into SHA.AREACODE ("TYPE", CODE, NAME, PARENT_CODE, SHORT_CODE, "CATALOG", SUB)"
    -- 测试时间
    values(current timestamp)
    ;

    -- 分批次修改VERSION 和 DARTETIME
    SELECT SUBSTR(CODE,1,1),count(1) FROM AREACODE a GROUP BY SUBSTR(CODE,1,1) ;
    UPDATE AREACODE SET VERSION ='2019',DARTETIME =(current timestamp) WHERE SUBSTR(CODE,1,1)='1' ;
    UPDATE AREACODE SET VERSION ='2019',DARTETIME =(current timestamp) WHERE SUBSTR(CODE,1,1)='2' ;
    UPDATE AREACODE SET VERSION ='2019',DARTETIME =(current timestamp) WHERE SUBSTR(CODE,1,1)='3' ;
    UPDATE AREACODE SET VERSION ='2019',DARTETIME =(current timestamp) WHERE SUBSTR(CODE,1,1)='4' ;
    UPDATE AREACODE SET VERSION ='2019',DARTETIME =(current timestamp) WHERE SUBSTR(CODE,1,1)='5' ;
    UPDATE AREACODE SET VERSION ='2019',DARTETIME =(current timestamp) WHERE SUBSTR(CODE,1,1)='6' ;
    UPDATE AREACODE SET VERSION ='2019',DARTETIME =(current timestamp) WHERE SUBSTR(CODE,1,1)='7' ;
    -- 查询结果
    SELECT  * FROM AREACODE a 
    ;
    ```

# 保存 SHADB 镜像

```bash
# 保存镜像
docker commit db2server db2server/shadb
# 导出容器
docker export db2server > db2server.shadb.tar
# 导入容器
cat nginx.tar | docker import - importednginx:ilatest
```

# EFCore 链接 db2

dotnet ef dbcontext scaffold "Server=192.168.31.180;Database=SHADB;password=sha;uid=sha;"  IBM.EntityFrameworkCore  
