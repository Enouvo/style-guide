# Why Git Code Reviews Are Important
## **Why Git Code Reviews Are Important**

Git code reviews are important for many reasons:

- Make sure the code works and meets requirements ([automated testing](https://www.perfecto.io/platform-page-test-creation) and [linting](https://gitlab.enouvo.com/enouvo-packages/enouvo-eslint-config) with Eslint can help this).
- Coaching new developers.
- Ensuring transparency across teams.
- Sharing innovation.
- Improving performance.

Doing these reviews properly can save time in the long term. It will help you identify bugs and improve quality earlier in development — before testing begins.

## Merge request **guidelines**

- Have self-reviewed this MR per [code review guidelines](https://docs.gitlab.com/ee/development/code_review.html).
- Choose the template default when you create merge request

![Untitled](https://enouvogroup.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F74779172-7a5e-49b2-b255-0a13361e9ce4%2FUntitled.png?id=fdf00da4-fa8b-4926-9b4d-8e8971f3f411&table=block&spaceId=6ab481b3-fa3f-4443-9b2d-075e46fafc3d&width=2000&userId=&cache=v2)

- The merge request have assign reviewer, and have title with format 
( [fix, feat](ticket number): message)
![Untitled](https://enouvogroup.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F0c70fcf9-bbbd-493e-89d1-6978e4fe31a3%2FUntitled.png?id=37ba51c4-4506-474d-a51a-b63a85f4dbb1&table=block&spaceId=6ab481b3-fa3f-4443-9b2d-075e46fafc3d&width=2000&userId=&cache=v2)
- Please refer the [link](docs/docs/review-check-list.md) to learn more about code check list
- Your request has to pass all lint, tests before submitting to the reviewers.
- If your request has some UI changes, let screenshot the change add attach this to the MR.
- If your request has conflict, let discuss this with all of the team related to this task.
- If the reviewer has some feedback, let a comment below the line code have an issue.

![Untitled](https://enouvogroup.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F8f5b3229-dfdb-4877-a9e1-7619c1df85d8%2FUntitled.png?id=d565c6dd-fb0b-4d30-9c6a-f1684a795d8b&table=block&spaceId=6ab481b3-fa3f-4443-9b2d-075e46fafc3d&width=2000&userId=&cache=v2)

- After comment let add the tag [WIP] to make sure this MR will be updated.

![Untitled](https://enouvogroup.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fa96a8f97-48e1-4a6d-b862-10b9cb1046ac%2FUntitled.png?id=a2487917-dd16-4659-9370-9a0d83154903&table=block&spaceId=6ab481b3-fa3f-4443-9b2d-075e46fafc3d&width=2000&userId=&cache=v2)

- The Team members should peer review the changes first, before submit to the reviewers.
- Your request would be merged by the reviewer if at least one reviewer approved the changes.
