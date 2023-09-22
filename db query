**Find all the topics which are thought in the month of October**

    db.topics.find({$and:[{topic_date:{$gt: new Date("30-sep-2022")}},{topic_date: {$lt: new Date("1-nov-2022")}}]})
    
    
**Find all the company drives which appeared between 15 oct-2020 and 31-oct-2020**

    db.companydrives.find({$and:[{ drive_date:{$gt: new Date("15-oct-2020")}},{ drive_date: {$lt: new Date("31-oct-2022")}}]})
    
    
**Find all the company drives and students who are appeared for the placement?**

    db.companydrives.aggregate([
        {
          $lookup: {
            from: "students",
            localField: "userid",
            foreignField: "userid",
            as: "userinfo",
          },
        },
        {
          $project: {
            _id: 0,
            "userinfo.name": 1,
            company: 1,
            drive_date: 1,
            "userinfo.email": 1,
            "userinfo.userid": 1,
          },
        },
      ]);
      
 
 **Find the number of problems solved by the user in codekata ?**
 
    db.codekata.aggregate([
        {
          $lookup: {
            from: "students",
            localField: "userid",
            foreignField: "userid",
            as: "userinfo",
          },
        },
        {
          $project: {
            _id: 0,
            userid: 1,
            problems: 1,
            "userinfo.name": 1,
          },
        },
      ]);
      
      
**Find all the mentors with who has the mentee's count more than 15 ?**

    db.students.aggregate([
        {
          $lookup: {
            from: "mentors",
            localField: "mentorid",
            foreignField: "mentorid",
            as: "mentorInfo",
          },
        },
        {
          $group: {
            _id: {
              mentorid: "$mentorInfo.mentorid",
              mentorname: "$mentorInfo.mentorname",
            },
            mentee_count: { $sum: 1 },
          },
        },
        { $match: { mentee_count: { $gt: 15 } } },
      ]);
      
      
**Find the number of users who are absent and task is not submitted  between 15 oct-2020 and 31-oct-2020**

    db.attendance.aggregate([
        {
          $lookup: {
            from: "topics",
            localField: "topicid",
            foreignField: "topicid",
            as: "topics",
          },
        },
        {
          $lookup: {
            from: "tasks",
            localField: "topicid",
            foreignField: "topicid",
            as: "tasks",
          },
        },
        { $match: { $and: [{ attended: false }, { "tasks.submitted": false }] } },
        {
          $match: {
            $and: [
              {
                $or: [
                  { "topics.topic_date": { $gte: new Date("15-oct-2020") } },
                  { "topics.topic_date": { $lte: new Date("31-oct-2020") } },
                ],
              },
              {
                $or: [
                  { "tasks.due_date": { $gte: new Date("15-oct-2020") } },
                  { "tasks.due_date": { $lte: new Date("31-oct-2020") } },
                ],
              },
            ],
          },
        },
        {
          $count: "No_of_students_absent",
        },
      ]);
