---
title: 【OSurges开源日记】Maven开源工程管理，工程目标
date: 2018-11-22 14:20:08
categories: OSurges
tags:
  - OSurges
  - 开源
---

OSurges 微服务开源框架正式启动。本文主要介绍maven工程围绕开源项目为目标，应具备的配置规范及代码质量管理，中央仓库等插件。

<!-- more -->

# 目标

- 工程名称、描述、已经开源地址
- 组织信息
- 开源协议
- 开发者信息
- scm部署管理
- issue问题跟踪管理
- properties
- 依赖管理
- 插件管理
- 统一配置

# pom.xml

> 说明将写在pom.xml文件的注释中。

```xml
<plugin>
    <groupId>org.jacoco</groupId>
    <artifactId>jacoco-maven-plugin</artifactId>
    <version>${jacoco-maven-plugin.version}</version>
    <executions>
        <execution>
            <id>pre-unit-tests</id>
            <goals>
                <goal>prepare-agent</goal>
            </goals>
        </execution>
        <execution>
            <id>check</id>
            <goals>
                <goal>check</goal>
            </goals>
        </execution>
        <execution>
            <id>report</id>
            <phase>prepare-package</phase>
            <goals>
                <goal>report</goal>
            </goals>
        </execution>
    </executions>
    <configuration>
        <rules>
            <rule implementation="org.jacoco.maven.RuleConfiguration">
                <element>BUNDLE</element>
                <limits>
                    <!-- 方法覆盖率 -->
                    <limit implementation="org.jacoco.report.check.Limit">
                        <counter>METHOD</counter>
                        <value>COVEREDRATIO</value>
                        <minimum>0.80</minimum>
                    </limit>
                    <!-- 指定覆盖率 -->
                    <limit implementation="org.jacoco.report.check.Limit">
                        <counter>INSTRUCTION</counter>
                        <value>COVEREDRATIO</value>
                        <minimum>0.80</minimum>
                    </limit>
                    <!-- 行覆盖率 -->
                    <limit implementation="org.jacoco.report.check.Limit">
                        <counter>LINE</counter>
                        <value>COVEREDRATIO</value>
                        <minimum>0.80</minimum>
                    </limit>
                    <!-- 类覆盖率 -->
                    <limit implementation="org.jacoco.report.check.Limit">
                        <counter>CLASS</counter>
                        <value>MISSEDCOUNT</value>
                        <maximum>0</maximum>
                    </limit>
                </limits>
            </rule>
        </rules>
    </configuration>
</plugin>
```

