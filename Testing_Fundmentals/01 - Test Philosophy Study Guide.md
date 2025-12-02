# Test Philosophy Study Guide

## Testing Mindset

### Tester Mindset
Testers are problem-oriented, concentrating on identifying issues and potential failures in software and the surrounding resources. Their goal is to ensure the application works under various conditions, often thinking about how to break the system to uncover weaknesses and vulnerabilities. They adopt the user’s perspective to test for real-world scenarios and usability, aiming to ensure the software meets quality standards and is free of defects. Their focus is on quality assurance, making sure the final product is reliable and intuitive

### Developer Mindset
Developers are primarily goal-oriented, focusing on building and implementing features that are functional, efficient, and scalable. They approach problems with a solution-focused mindset, always thinking about how to make things work. Attention to detail is crucial for them, as they strive to write clean, efficient code that performs well. They also assess risks in terms of technical challenges, scalability, and performance, ensuring that the software can handle its use demands

## Why Test

### Objectives of Testing
Your test context will guide your natural test objectives, but there are some common objects that can be targeted in most contexts:
- Evaluating work products (requirements, code, etc)
- Finding defects
- Checking coverage of a test object
- Reducing risk of poor software quality
- Verifying requirements have been met
- Providing metrics to stakeholders
- Building confidence in the quality of the test object

### Quality Management
Despite the terms testing and **quality assurance** (**QA**) often being used synonymously, they are actually distinct concepts. Testing is a form of **quality control** (**QC**) that is product-oriented and corrective, focused on identifying and fixing defects to achieve high levels of quality. **QA**, on the other hand, is process-oriented and preventive, aiming to improve processes to ensure high quality results. This means that testing itself is a **QC** practice, whereas **QA** involves implementing and improving processes, ensuring that good processes lead to good products. Test results are used in **QC** to fix defects, and in **QA** to provide feedback on process performance

### Requirements
**Requirements** can vary widely, encompassing business, technical, regulatory, accessibility, and other arbitrary needs. They provide details about what should be included or excluded from a product. These **requirements** can take many forms, although there are some standardized methods for presenting them. Common formats include software requirement specifications, use cases, user stories, and non-functional specifications. Each of these formats helps ensure that all necessary aspects of the product are clearly defined and understood by developers, testers, and any other stakeholders

### Verification & Validation
Most testing can be categorized as either **verification** or **validation**. These two categories of tests have different objectives:
- **verification** answers the question "are we building the product correctly?"
- **validation** answers the question "are we building the right product?"

For example, imagine you are on a team that has been tasked with building and testing a bike. **Verification** would involve checking that each component of the bike meets the specified design requirements and standards. This could involve checking the frame is made from the correct material, the brakes are designed properly, the correct number of gears are accommodated in the plan, etc. Essentially, verification is about confirming that the bike is being assembled according to any provided requirements through the use of **static testing**. On the other hand, **validation** would involve testing the bike in real-world conditions to ensure it meets the needs and expectations of the end user. This might include taking the bike for a test ride to confirm it provides a comfortable and safe riding experience, and that it performs well under various conditions such as different terrains and weather. **Validation** ensures that the final product is fit for its intended purpose and satisfies customer requirements through the use of **dynamic testing**.

## Testing Principles
- **Testing Reveals Defects, Not their absence**
    - 0 defects discovered does not mean the*re are no defects in the tested software
- **Exhaustive Testing is not possible**
    - testing should be focused on critical features/requirements first
- **Test early**
    - the sooner testing is started the earlier defects will be caught
        - static testing should start as soon as possible
        - dynamic testing should be started when feasible
- **Defects Cluster**
    - any feature/requirement with one or more defects warrants extra testing
    - defects tend to cascade, especially if the defect is at the start of any data transformation or if other features require the data involved in the defect
- **Tests Wear Out**
    - your tests will eventually exhaust all defects they can find: when this happens it is worth considering additional tests to accommodate the addition of new features or requirements
    - don't remove old tests when they stop discovering defects: you can still use them for regression testing
- **Testing is Contextual**
    - there is no overarching universal testing practice: your test objects and objectives should determine how you approach the testing process
- **Absence of Error Fallacy**
    - just because there are no defects does not mean your application was built correctly
        - all tests may pass, but the application may not meet all client requirements