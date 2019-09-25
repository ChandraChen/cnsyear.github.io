---
title: 使用JDBC在MySQL数据库中快速批量插入十万级的数据
description: 
categories:
 - 疑难杂症
tags:
 - 疑难杂症
 - JDBC
---

> 原先的项目使用的Hibernate框架进行数据的操作，今天遇到一个问题那就是当插入大量的数据时。使用for循环一条条的插入效率很低，速度很慢。。。。。最后没办法直接使用原生的jdbc直接往数据库了干，果真效率快的不是一点半点。。。。。

<!--more-->

jdbc怎么配置就不说了，会的人直接看下面的代码。。
```Java
package cn.com.highset.dao;  
  
import java.io.BufferedReader;  
import java.io.FileInputStream;  
import java.io.IOException;  
import java.io.InputStreamReader;  
import java.sql.Connection;  
import java.sql.DriverManager;  
import java.sql.PreparedStatement;  
import java.sql.SQLException;  
import java.sql.Timestamp;
import java.sql.Types;
import java.util.List;

import cn.com.highset.util.HighsetInit;
import cn.com.highset.util.NaNN;
 
/**
 *  使用JDBC在MySQL数据库中快速批量插入数据
 *  
 * @author JIE.ZHAO
 * @date 2017年5月16日 下午3:19:18
 */
public class DbStoreHelper {  
  
    private String insert_sql;  
    private String charset;  
    private boolean debug;  
  
    private String jdbc;  
    private String connectStr;  
    private String username;  
    private String password;  
  
	public DbStoreHelper(String insert_sql) {
		/**
		 * useServerPrepStmts=false，如果不开启(useServerPrepStmts=false)，使用com.mysql.
		 * jdbc.PreparedStatement进行本地SQL拼装，最后送到db上就是已经替换了?后的最终SQL.
		 */
		connectStr = HighsetInit.getProperty("JDBC_URL") + "?characterEncoding=utf8&useServerPrepStmts=false&rewriteBatchedStatements=true";
		// connectStr +=
		// "?useServerPrepStmts=false&rewriteBatchedStatements=true";
		this.insert_sql = insert_sql;
		jdbc = HighsetInit.getProperty("JDBC");
		charset = HighsetInit.getProperty("JDBC_CHARSET");
		username = HighsetInit.getProperty("JDBC_USERNAME");
		password = HighsetInit.getProperty("JDBC_PASSWORD");
	}
  
    public void storeToDb(String srcFile) throws IOException {  
        BufferedReader bfr = new BufferedReader(new InputStreamReader(new FileInputStream(srcFile), charset));  
        try {  
            doStore(bfr);  
        } catch (Exception e) {  
            e.printStackTrace();  
        } finally {  
            bfr.close();  
        }  
    }  
  
    private void doStore(BufferedReader bfr) throws ClassNotFoundException, SQLException, IOException {  
        Class.forName("com.mysql.jdbc.Driver");  
        Connection conn = DriverManager.getConnection(connectStr, username,password);  
        conn.setAutoCommit(false); // 设置手动提交  
        int count = 0;  
        PreparedStatement psts = conn.prepareStatement(insert_sql);  
        String line = null;  
        while (null != (line = bfr.readLine())) {  
            String[] infos = line.split(";");  
            if (infos.length < 5)   continue;  
            if (debug) {  
                System.out.println(line);  
            }  
            psts.setLong(1, Long.valueOf(infos[0]));  
            psts.setLong(2, Long.valueOf(infos[1]));  
            psts.setString(3, infos[2]);  
            psts.setString(4, infos[3]);  
            psts.setString(5, infos[4]);  
            psts.addBatch();// 加入批量处理  
            count++;              
        }  
        psts.executeBatch(); // 执行批量处理  
        conn.commit();  // 提交  
        System.out.println("All down : " + count);  
        conn.close();  
    }  
  
    /**
     * 传sql
     */
    private void doStore(List<String> sqlList) throws ClassNotFoundException, SQLException, IOException {  
        Class.forName(jdbc);  
        Connection conn = DriverManager.getConnection(connectStr, username,password);  
        conn.setAutoCommit(false); // 设置手动提交  
        int count = 0;  
        PreparedStatement psts = conn.prepareStatement(insert_sql);  
        for (int i = 0; i < sqlList.size(); i++) {
        	count++;
        	String[] infos = sqlList.get(i).split(",");
    	 	setValue(psts,1,infos[0],Types.INTEGER);//Integer task_id;// 任务名称
    	 	setValue(psts,2,infos[1],Types.VARCHAR);//String xh;// 序号
    		setValue(psts,3,infos[2],Types.INTEGER);//Integer zyxh1;// 专业序号1
    		setValue(psts,4,infos[3],Types.INTEGER);//Integer zyxh2;// 专业序号2
    		setValue(psts,5,infos[4],Types.INTEGER);//Integer zyxh3;// 专业序号3
    		setValue(psts,6,infos[5],Types.INTEGER);//Integer zyxh4;// 专业序号4
    		setValue(psts,7,infos[6],Types.INTEGER);//Integer zyxh5;// 专业序号5
    		setValue(psts,8,infos[7],Types.INTEGER);//Integer zyxh6;// 专业序号6
    		setValue(psts,9,infos[8],Types.INTEGER);//Integer tdzy;// 投档专业(投档志愿）
    		setValue(psts,10,infos[9],Types.VARCHAR);//String ksh;// 考生号
    		setValue(psts,11,infos[10],Types.VARCHAR);//String xm;// 姓名
    		setValue(psts,12,infos[11],Types.INTEGER);//Integer xbdm;// 性别代码
    		setValue(psts,13,infos[12],Types.DOUBLE);//Double tdcj;// 投档成绩
    		setValue(psts,14,infos[13],Types.VARCHAR);//String csny;// 出生年月
    		setValue(psts,15,infos[14],Types.INTEGER);//Integer lqzy;//
    		setValue(psts,16,infos[15],Types.VARCHAR);//String lqzy_a;// 录取专业—a
    		setValue(psts,17,infos[16],Types.VARCHAR);//String lqzy_b;// 录取专业—b
    		setValue(psts,18,infos[17],Types.VARCHAR);//String jhs;// 计划数（艺术类）
    		setValue(psts,19,infos[18],Types.VARCHAR);//String zxmc;// 中学名称
    		setValue(psts,20,infos[19],Types.VARCHAR);//String sfzh;// 身份证号
    		setValue(psts,21,infos[20],Types.VARCHAR);//String jtdz;// 家庭地址
    		setValue(psts,22,infos[21],Types.VARCHAR);//String yzbm;// 邮政编码
    		setValue(psts,23,infos[22],Types.VARCHAR);//String lxdh;// 联系电话
    		setValue(psts,24,infos[23],Types.VARCHAR);//String sjr;// 收件人
    		setValue(psts,25,infos[24],Types.INTEGER);//Integer mzdm;// 民族代码
    		setValue(psts,26,infos[25],Types.INTEGER);//Integer wyyzdm;// 外语语种代码
    		setValue(psts,27,infos[26],Types.INTEGER);//Integer zzmmdm;// 政治面貌代码
    		setValue(psts,28,infos[27],Types.INTEGER);//Integer syd;// 生源地
    		setValue(psts,29,infos[28],Types.VARCHAR);//String xymc;// 学院名称
    		setValue(psts,30,infos[29],Types.VARCHAR);//String xq;// 校区
    		setValue(psts,31,infos[30],Types.INTEGER);//Integer klmc;// 科类名称
    		setValue(psts,32,infos[31],Types.INTEGER);//Integer pc;// 批次
    		setValue(psts,33,infos[32],Types.VARCHAR);//String sbkx;// 省本科线
    		setValue(psts,34,infos[33],Types.INTEGER);//Integer enabled;// 状态(1:有效)
    		setValue(psts,35,infos[34],Types.TIMESTAMP);//Timestamp create_time;// 创建时间
    	    setValue(psts,36,infos[35],Types.INTEGER);//Integer create_user_id;// 创建人id
            psts.addBatch();// 加入批量处理  
		}
        psts.executeBatch(); // 执行批量处理  
        conn.commit();  // 提交  
        System.out.println("All down : " + count);  
        conn.close();  
    }  
    
    private void setValue(PreparedStatement psts, int i, String infos ,int type) throws NumberFormatException, SQLException {
    	 if("null".equals(infos)||NaNN.isNull(infos)){
    		switch (type) {
				case Types.INTEGER :
					 psts.setNull(i, Types.INTEGER);
					break;
				case Types.DOUBLE :
					psts.setNull(i, Types.DOUBLE);
					break;
				case Types.VARCHAR :
					psts.setNull(i, Types.VARCHAR);
					break;
				case Types.TIMESTAMP :
					psts.setNull(i, Types.TIMESTAMP);
					break;
				default :
					break;
			}
    	 }else{
    		 switch (type) {
 				case Types.INTEGER :
 					 psts.setInt(i,Integer.parseInt(infos)); 
 					break;
 				case Types.DOUBLE :
 					psts.setDouble(i,Double.parseDouble(infos)); 
 					break;
 				case Types.VARCHAR :
 					 psts.setString(i,infos); 
 					break;
 				case Types.TIMESTAMP :
 					psts.setTimestamp(i,new Timestamp(System.currentTimeMillis())); 
 					break;
 				default :
 					break;
 			}
    		
    	 }
		
	}

	public void storeSqlToDb(List<String> sqlList) throws IOException {  
        try {  
        	doStore(sqlList);  
        } catch (Exception e) {  
            e.printStackTrace();  
        }
    }  
    
}  


```


 

