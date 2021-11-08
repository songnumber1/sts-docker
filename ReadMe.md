# 수동 배포 방법

## docker:build

1.  프로젝트 선택
2.  run - maven build
3.  Goals : docker:build 후 run
4.  오류가 발생 시 아래 jar 파일 생성 후 다시 실행
5.  docker images에서 pom.xml에 작성한 song/stsdocker 이름으로 추가되었는지 확인

## jar 파일 생성

1.  프로젝트 선택
2.  run - maven build
3.  Goals : package 후 run
4.  프로젝트 루트/target 폴더에 jar 파일 생성 확인 및 sts boot 콘솔에서 빌드 정상 확인

<note>아래는 pom.xml에 sts docker plugin 추가 부분이다.</note>

<code>

        <plugin>
            <groupId>io.fabric8</groupId>
            <artifactId>docker-maven-plugin</artifactId>
            <version>0.37.0</version>
            <configuration>
                <images>
                    <image>
                        <name>song/stsdocker</name>
                        <build>
                            <dockerFileDir>${basedir}</dockerFileDir>
                        </build>
                    </image>
                </images>
            </configuration>
        </plugin>
    </plugins>

</code>

# 자동 배포

## jar 파일 생성

1.  프로젝트 선택
2.  run - maven build
3.  Goals : clean package 후 run
4.  sts boot 콘솔에서 빌드 정상 확인 및 도커 이미지 추가 생성 또는 이미지 갱신 시간 확인

<note>아래는 pom.xml에 sts docker plugin 추가 부분이다.</note>

<code>

        <plugin>
            <groupId>io.fabric8</groupId>
            <artifactId>docker-maven-plugin</artifactId>
            <version>0.37.0</version>
            <configuration>
                <images>
                    <image>
                        <name>song/stsdocker</name>
                        <build>
                            <dockerFileDir>${basedir}</dockerFileDir>
                        </build>
                    </image>
                </images>
            </configuration>
            <executions>
                <execution>
                    <id>docker-build</id>
                    <phase>package</phase>
                    <goals>
                        <goal>build</goal>
                    </goals>
                </execution>
            </executions>
        </plugin>

</code>

<note>fabric8 공식 문서 링크 : http://dmp.fabric8.io/#docker:build</note>
