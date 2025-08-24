---
layout: textbook
title: "Guardians of the Machine: AI Ethics, Welfare, and Rights - Survey of ethical frameworks (utilitarianism, deontology, virtue ethics)"
date: 2025-08-24T04:14:09.352280
study_plan_url: "https://lumorikllc.github.io/learn/content/00000000-0000-0000-0000-000000000000/4a909e71-4c9d-47fa-bfa6-b59c87074d17/"
chapters: 8
author: "00000000-0000-0000-0000-000000000000"
description: "AI-generated textbook by Lumorik"
---

## Chapter Overview
Choosing how to evaluate AI behavior isn’t just a technical decision—it’s a moral one. Different ethical frameworks yield different guidance on what makes AI systems *right* or *wrong*.

By the end of this chapter, you should be able to:
- Identify and compare the three major ethical frameworks: utilitarianism, deontology, and virtue ethics.  
- Analyze ethical dilemmas from each framework’s perspective.  
- Apply these theories to real-world AI development scenarios.

## Key Concepts & Definitions
**Ethical Framework**: A structured approach for evaluating the moral rightness of actions.  
**Consequentialism**: Moral theory judging actions solely by their outcomes.  
**Utilitarianism**: Consequentialist view maximizing overall happiness or utility.  
**Act Utilitarianism**: Evaluates each individual act by its net utility.  
**Rule Utilitarianism**: Follows rules that generally maximize utility.  
**Deontology**: Duty-based theory focusing on rules rather than outcomes.  
**Categorical Imperative**: Kant’s principle: act only by maxims you’d will universal.  
**Virtue Ethics**: Focuses on character traits (virtues) leading to human flourishing.  
**Eudaimonia**: Aristotle’s term for a flourishing, fulfilled life.  

These frameworks interrelate by offering alternate answers to “What makes an action moral?” Consequentialism (utilitarianism) looks at results, deontology stresses duties, and virtue ethics emphasizes moral character. Together they form a toolkit for evaluating AI designs.

## Main Exposition

### 1. Utilitarianism
Utilitarianism judges actions by their *net utility*—usually happiness or welfare.  
- **Founders**: Jeremy Bentham introduced “greatest happiness for the greatest number.” John Stuart Mill refined qualitative differences in pleasures.  
- **Utility Calculation**:  
  $$U = \sum_{i=1}^n u_i$$  
  where $u_i$ is the utility of outcome _i_.  
- **Act vs. Rule**:  
  - *Act Utilitarianism* calculates $U$ case by case.  
  - *Rule Utilitarianism* endorses rules whose general adoption maximizes $U$.  
- **Strength**: Flexible, outcome-focused.  
- **Weakness**: Can justify rights violations if utility is high enough.

### 2. Deontology
Deontological ethics holds some actions are intrinsically right or wrong, regardless of consequences.  
- **Immanuel Kant**: Key figure who introduced the *Categorical Imperative*.  
- **First Formulation**: "Act only on maxims you can will to become universal law."  
- **Second Formulation**: "Treat humanity, in yourself or others, always as an end and never merely as a means."  
- **Strength**: Respects individual rights and duties.  
- **Weakness**: Can lead to rigid choices that ignore beneficial outcomes.

### 3. Virtue Ethics
Virtue ethics shifts focus from *actions* to *character*.  
- **Origin**: Aristotle’s *Nicomachean Ethics*.  
- **Virtues**: Traits like courage, temperance, honesty.  
- **Golden Mean**: Virtue lies between deficiency and excess (e.g., courage is between cowardice and recklessness).  
- **Eudaimonia**: The goal of living well, achieved by cultivating virtues.  
- **Strength**: Encourages moral development and context sensitivity.  
- **Weakness**: Offers less clear action-guidance in novel situations.

## Applications & Real-World Context

**Scenario 1: Self-Driving Car Dilemma**  
A self-driving car must choose between swerving into a barrier (harming the passenger) or staying its course (harming two pedestrians).  
- *Utilitarianism* calculates total lives saved (2 vs. 1) and chooses to swerve.  
- *Deontology* applies a rule forbidding intentional harm to an innocent bystander—hence it cannot swerve.  
- *Virtue Ethics* asks what a *prudent* or *compassionate* driver would do, balancing care for passengers and pedestrians.

**Scenario 2: Content-Moderation AI**  
An AI flags user speech for hate content.  
- *Utilitarianism* weighs the social harm of unchecked hate vs. free-speech value.  
- *Deontology* checks compliance with a rule: “Never silence legitimate political discourse.”  
- *Virtue Ethics* asks whether the system reflects moderation virtues like fairness and respect.

**Scenario 3: Hiring Algorithm**  
An AI recruiting tool ranks candidates.  
- *Utilitarianism* optimizes workforce productivity across the company.  
- *Deontology* ensures rules against discrimination are strictly enforced.  
- *Virtue Ethics* promotes honesty and equity in candidate evaluation.

## Common Misconceptions & Pitfalls
1. Misconception: “Utilitarianism always demands total sacrifice.”  
   Correction: It balances aggregate utility; small sacrifices may not outweigh greater benefits.
2. Misconception: “Deontology ignores outcomes entirely.”  
   Correction: It prioritizes rules but still recognizes context when defining duties.
3. Misconception: “Virtue ethics has no action guidance.”  
   Correction: It uses practical wisdom (*phronesis*) to navigate specific situations.
4. Misconception: “Rule utilitarianism and deontology are the same.”  
   Correction: Rule utilitarianism endorses rules for outcomes; deontology endorses rules from duty regardless of aggregate utility.

## Worked Example Problem
**Problem:**  
A delivery drone must divert from its route to avoid striking a child on the ground, but diversion delays a medical kit delivery, risking three patients’ lives. Decide according to each framework.

**Solution Steps:**
1. **Utilitarian Calculation**  
   - Lives at risk if on-route: 3 patients. Lives saved by diversion: 1 child.  
   - Net lives = $+1 - 3 = -2$.  
   - *Conclusion*: Do not divert (maximize total lives).
2. **Deontological Rule**  
   - Rule A: “Do not intentionally act to kill.”  
   - Rule B: “Keep medical deliveries on time.”  
   - Conflicting duties—Kantian solution rejects harming the child, so divert.
3. **Virtue Ethics Analysis**  
   - Identify virtues: compassion (save the child), justice (deliver medicine).  
   - Practical wisdom suggests partial diversion: slow down but broadcast an alert.  
   - *Conclusion*: Seek creative compromise.

**Commentary:**  
Each step shows how the framework’s focus—outcome totals, duty consistency, or character deliberation—yields different actions.

## Practice Exercises
Q1. Define *act utilitarianism* and *rule utilitarianism*.  
Q2. State Kant’s first formulation of the *Categorical Imperative*.  
Q3. Give an example of a virtue and describe its golden mean.  
Q4. A content-filtering AI must block 10% of hate speech and minimize free-speech harm. How might a utilitarian vs. deontologist approach differ?  
Q5. In 50 words, explain why virtue ethics emphasizes *eudaimonia* over individual acts.

## Summary & Further Reading
- Utilitarianism judges actions by aggregate utility, with act and rule variants.  
- Deontology stresses duties and universal moral law, respecting persons as ends.  
- Virtue ethics centers on cultivating good character traits and human flourishing.  
- Each framework provides unique guidance—and unique challenges—for AI design.  
- Real-world AI dilemmas (e.g., self-driving cars) reveal trade-offs among outcomes, rules, and virtues.

Annotated Bibliography:
- Bentham, J. (1789). *An Introduction to the Principles of Morals and Legislation*. Foundational utilitarian theory.  
- Kant, I. (1785). *Groundwork of the Metaphysics of Morals*. Key source for deontological ethics.  
- Aristotle. *Nicomachean Ethics*. Classic work establishing virtue ethics and *eudaimonia*.  
- Mill, J. S. (1863). *Utilitarianism*. Refines qualitative distinctions in pleasure.  
- Slote, M. (2010). *Morality for Humans*. Modern overview of virtue ethics applied to technology.

## Solutions
**Q1.** Act utilitarianism evaluates each individual act by its immediate utility; rule utilitarianism upholds rules that tend to maximize utility when generally followed.  
**Q2.** “Act only on that maxim whereby you can at the same time will that it should become a universal law.”  
**Q3.** Example: *Courage* is the mean between *cowardice* (deficiency) and *recklessness* (excess).  
**Q4.** A utilitarian may block speech only if net social harm reduction exceeds free-speech loss; a deontologist follows a rule like “never censor legitimate expression,” regardless of total harm.  
**Q5.** Virtue ethics holds that moral worth lies in flourishing through virtues; *eudaimonia*—a complete, fulfilling life—is the ultimate aim beyond any single right act.