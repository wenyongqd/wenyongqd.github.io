---
title: 'Personal-Project-Management-Backend(2) '
date: 2020-05-20 15:29:30
tags:
---

## Backlog and ProjectTask Entiries
1. `Backlog.js`
```javascript
package io.igileintelliengence.ppmtool.domain;


import javax.persistence.Entity;
import javax.persistence.GeneratedValue;
import javax.persistence.GenerationType;
import javax.persistence.Id;

@Entity
public class Backlog {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    private Integer PTSequence = 0;
    private String projectIndetifier;

    //OneToOne with project

    //OneToMany projecttasks


    public Backlog() {
    }

    public Long getId() {
        return id;
    }

    public void setId(Long id) {
        this.id = id;
    }

    public Integer getPTSequence() {
        return PTSequence;
    }

    public void setPTSequence(Integer PTSequence) {
        this.PTSequence = PTSequence;
    }

    public String getProjectIndetifier() {
        return projectIndetifier;
    }

    public void setProjectIndetifier(String projectIndetifier) {
        this.projectIndetifier = projectIndetifier;
    }
}

```
2. `ProjectTask.js`
```javascript
ffggg
```