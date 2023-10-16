## 155. NoSQL

***

## 156. MongoDB

***

## 157. Installing Mongo

* [How to install a local MongoDB on macOS and connect to Studio 3T](https://studio3t.com/knowledge-base/articles/how-to-install-a-local-mongodb-on-macos/?kw=&cpn=20425562857&utm_source=adwords&utm_medium=ppc&utm_term=&utm_campaign=P-Max+%7C+Aug+23+%7C+USA&hsa_net=adwords&hsa_ad=&hsa_src=x&hsa_ver=3&hsa_grp=&hsa_acc=1756351187&hsa_tgt=&hsa_mt=&hsa_kw=&hsa_cam=20425562857&gad=1&gclid=Cj0KCQjwm66pBhDQARIsALIR2zDpdaTAluQY8jUICrwRUXJSMt_XNeUWwneMWxxWl5jhIyGYphjKrM8aAjSmEALw_wcB)

* [How to install Mongodb 5](https://www.youtube.com/watch?v=s1WQ0eEpqqg)

### Install brew
* [Homebrew](https://brew.sh/)
```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

```
$ brew -v
```

```
$ vim ~/.bash_profile
export PATH=$PATH:/opt/homebrew/bin
$ source ~/.bash_profile
```

```
$ brew update

$ brew upgrade
```

### Install `xcode`
```
$ xcode-select --install
```

### Install mongodb

```
$ brew tap mongodb/brew               # where to install that package from
```

```
$ brew install mongodb-community@6.0
```

```
$ brew services start mongodb-community@6.0
$ brew services stop  mongodb-community@6.0
```

```
$ brew services list
```

```
$ mongod --config /opt/homebrew/etc/mongod.conf --fork
```

```
$ mongosh

test> show dbs
```

```
$ mkdir -p /data/db
$ sudo chown -R 4(whoami) /data/db
```

***

## 158. Database

***

## 159. Collection

***

## 160. Document

***

## 161. Find(aka, query)

***

## 162. Update

***

## 163. Remove

***

## 164. Projection

***

## 165. Limit

***

## 166. Sort

***

## 167. Index

***

## 168. Aggregation

***

## 169. Users

***

## 170. JSON

***

## 171. Create Read Update Delete (CRUD)

***




































